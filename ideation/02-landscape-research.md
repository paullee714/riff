# Landscape research

Research checked: 2026-09-14. Sources are official project material; feature descriptions do not establish user demand or comparative performance.

| Reference | Layer and documented capability | Implication for our exploration |
| --- | --- | --- |
| [NGINX](https://nginx.org/en/) | HTTP server and reverse proxy, also supporting caching and load balancing; master/worker architecture | A replacement requires substantial operational breadth; start with a specific pain |
| [Tomcat architecture](https://tomcat.apache.org/tomcat-11.0-doc/architecture/overview.html) | Servlet container with connectors, an engine, hosts, and application contexts | Compatibility and application lifecycle are central to this direction |
| [Netty](https://netty.io/) | Asynchronous, event-driven framework for protocol clients and servers | A library needs an excellent developer API and clear concurrency behavior |
| [Caddy](https://caddyserver.com/) | Web server emphasizing automatic HTTPS | Simple configuration or automatic certificates alone are weak differentiation |

## Architectural reading

- [NGINX development guide](https://nginx.org/en/docs/dev/development_guide.html): study event handling and resource lifetimes.
- [Netty user guide](https://netty.io/wiki/user-guide.html): study handler composition and network application development.
- Tomcat's architecture page above: study separation between transport and application lifecycle.

## Unanswered competitive questions

Existing tools may already solve the proposed pain through metrics, tracing, logs, or extensions. Before writing a runtime, reproduce one overload incident using existing tooling and document what remains difficult. Compare equivalent deployment layers: a proxy benchmark does not establish that an application container or networking library is inferior.

Expand later to Envoy, HAProxy, Undertow, and language-native HTTP libraries after selecting the product layer. Their capabilities have not been evaluated in this initial pass.
