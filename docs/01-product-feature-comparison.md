# Product feature comparison

Research date: 2026-09-15. Riff is unimplemented. “Benchmark” in this document means capability comparison; measured performance work is planned separately.

## Compare the right layers

“Apache” here means Apache HTTP Server (httpd); Apache Tomcat is included separately. A deployable proxy, an application container, and a networking library are not interchangeable products.

| Product / documentation scope | Primary layer | Features to study | Riff relevance |
| --- | --- | --- | --- |
| Apache HTTP Server 2.4 | Web server / proxy | Modules, event MPM, proxy routing, HTTP/2 | Extensibility and operational compatibility |
| NGINX Open Source | Web server / proxy | Event-driven workers, static files, caching, balancing | Traffic handling and request lifecycle |
| Netty 4.2 API | JVM networking library | Handler pipeline, asynchronous I/O, read/write controls | Best direct reference for an embeddable toolkit |
| Tomcat 11 | Servlet application container | Application lifecycle, connectors, concurrency controls | JVM HTTP-service baseline |
| Caddy documentation | Web server / proxy | Automatic HTTPS, configuration experience | Setup friction baseline |
| HAProxy 3.2 community guide | TCP/HTTP load balancer | ACLs, health checks, balancing, statistics | Failure handling and operations baseline |
| Envoy latest documentation | Service / edge proxy | Filters, circuit breakers, retries, observability | Existing sophisticated traffic controls |

Sources and caveats for each row follow. Latest Envoy documentation can include development features; pin a stable release before implementation comparison.

## Apache HTTP Server

The event MPM combines processes and threads, moving some connection work to listener threads so idle keep-alive connections need not each occupy a worker. Filters and processing paths can affect this behavior. Avoid the outdated claim that Apache always uses one blocking process per connection. [Event MPM documentation](https://httpd.apache.org/docs/2.4/mod/event.html)

Proxying is provided through modules; HTTP/2 has its own module/build requirements. This makes module selection part of a reproducible deployment. [mod_proxy](https://httpd.apache.org/docs/2.4/mod/mod_proxy.html), [HTTP/2 guide](https://httpd.apache.org/docs/2.4/howto/http2.html)

Our assessment: a broad module ecosystem is useful but expensive to reproduce. Riff should study explicit extension boundaries and configuration errors, rather than promise compatibility with arbitrary Apache modules.

## NGINX Open Source

NGINX documents static serving, reverse proxying, caching, load balancing, TLS, HTTP/2, HTTP/3, and TCP/UDP proxying. Its master/worker model and event-driven processing are central architectural references. Build and configuration affect enabled protocols. These statements refer to open-source documentation, not an assumption that NGINX Plus features are included. [NGINX capabilities](https://nginx.org/en/)

Our assessment: feature parity is too broad for an initial project. Study resource lifetimes, streaming, timeouts, configuration reloads, and usable diagnostics. A generic “faster NGINX” claim is unsupported.

## Netty

Netty is a library for building protocol clients and servers. ChannelPipeline composes inbound and outbound handlers; the application assembles its behavior. It is not a ready-made servlet container or an NGINX-style configured proxy. [Netty overview](https://netty.io/), [ChannelPipeline API](https://netty.io/4.2/api/io/netty/channel/ChannelPipeline.html)

ChannelConfig exposes automatic-read control and write-buffer watermarks. These are mechanisms developers must use correctly; they do not by themselves prove an application's entire memory footprint is bounded. [ChannelConfig API](https://netty.io/4.2/api/io/netty/channel/ChannelConfig.html)

Our assessment: strongest starting reference if Riff is a JVM library. A transport built on Netty must be compared with an equivalent Netty application to isolate Riff's added value and overhead.

## Apache Tomcat

Tomcat organizes an application container through connectors, an engine, hosts, and application contexts. It targets Servlet compatibility. HTTP connector settings expose controls including connection limits, request-processing threads, and the accept queue; details depend on connector and executor configuration. [Architecture](https://tomcat.apache.org/tomcat-11.0-doc/architecture/overview.html), [HTTP connector](https://tomcat.apache.org/tomcat-11.0-doc/config/http.html)

Our assessment: a useful HTTP application baseline. Servlet support brings compatibility and lifecycle obligations. Riff should not call itself a drop-in replacement without defining and testing those obligations.

## Caddy

Caddy's automatic HTTPS obtains and renews certificates and configures HTTP-to-HTTPS redirects under documented conditions. Local names and public certificates follow different paths and requirements. [Automatic HTTPS](https://caddyserver.com/docs/automatic-https)

Our assessment: setup experience is already a competitive strength in this space. A pleasant config file alone is insufficient differentiation. Test time to a working service, understandable errors, and recovery after a bad configuration.

## HAProxy

The community guide covers TCP/HTTP balancing, TLS, health monitoring, ACLs, stick tables, server protection, logs, statistics, and runtime management. It is primarily a traffic intermediary, not an application-hosting framework. Enterprise add-ons are outside this comparison. [HAProxy 3.2 starter guide](https://docs.haproxy.org/3.2/intro.html)

Our assessment: use as a proxy resilience baseline, especially upstream failures and capacity handling. Do not compare its forwarding path directly with Riff running application business logic.

## Envoy

Envoy documents filtering, service discovery, load balancing, retries, outlier detection, and observability. Circuit breaking can bound upstream resources such as connections or requests; exact semantics and counters are version-sensitive. [Envoy overview](https://www.envoyproxy.io/docs/envoy/latest/intro/what_is_envoy), [Circuit breaking](https://www.envoyproxy.io/docs/envoy/latest/intro/arch_overview/upstream/circuit_breaking)

Our assessment: “has circuit breakers and metrics” is already established territory. Riff's potential advantage must be the developer workflow or a focused deployment use case, demonstrated against existing tooling.

## Feature priorities inferred for Riff

| Area | First prototype | Later / contingent |
| --- | --- | --- |
| Transport | Existing HTTP implementation, streaming, explicit deadlines | More protocols after a user need is demonstrated |
| Resource control | Active-work limit, bounded waiting, body limits | Adaptive policies after fixed policies are understood |
| Developer API | Small handler API and explicit execution model | Extension ecosystem after API feedback |
| Diagnostics | Queue wait, handler time, timeout/rejection reason | Distributed tooling integrations after one local incident works |
| Operations | Validated configuration and graceful drain | Reload and certificate management if Riff becomes a standalone server |
| Compatibility | State exactly what is supported | Servlet or proxy compatibility only as a deliberate product choice |

All rows are proposed scope, not implemented features. Language selection remains open.
