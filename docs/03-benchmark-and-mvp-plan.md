# Benchmark and MVP plan

Date: 2026-09-15. Proposed experiments only. No throughput, latency, reliability, or usability results exist for Riff.

## Keep separate comparison tracks

| Track | Candidates | Same work required |
| --- | --- | --- |
| Embedded HTTP application | Riff, minimal Netty application, Tomcat application | Same payload, handler work, serialization, and resource limits |
| Reverse proxy | Riff only if it implements proxying; Apache httpd, NGINX, Caddy, HAProxy, Envoy | Same upstream, routing, TLS policy, and response |
| Protocol toolkit | Riff only if selected; Netty | Same framing, buffer behavior, client, and protocol semantics |

A product outside a track is not scored as missing a feature it was not designed to provide. Avoid one universal winner table.

## Workloads

- Small fixed response and representative JSON handler: establish normal service overhead.
- Slow application work: observe queuing, deadlines, and capacity rejection.
- Slow upload/download: observe streaming, buffer limits, and cancellation.
- Burst beyond capacity: measure accepted, rejected, failed, and timed-out requests separately.
- Upstream unavailable or slow: proxy track only; control retries and idempotency.
- Graceful shutdown during active traffic: verify admitted work drains to a deadline.
- Malformed and oversized requests: verify documented rejection behavior and resource release.

Correctness is a prerequisite. Do not improve throughput by omitting checks that the baseline performs.

## Measurement protocol

Pin release versions, dependencies, build flags, OS, CPU, memory, network topology, and all configuration files. Keep payloads, connection reuse, protocol, compression, TLS, and logging comparable. Warm up each runtime; use multiple repetitions and retain per-run data. Alternate run order to reduce environmental drift.

Use controlled arrival rates to examine overload and report offered load alongside achieved throughput. Check client saturation, coordinated omission, timeouts, and histogram semantics. Report p50/p95/p99, error/rejection rates, CPU, RSS, and recovery time. Explain the scope of every memory metric and queue limit.

A proxy cannot directly observe time inside a handler without application instrumentation. Only compare timing breakdowns measured with equivalent instrumentation; otherwise mark them unavailable.

## Developer-experience experiment

Give users the same incident and access to each product's normal documentation and telemetry. Measure time to a correct diagnosis, configuration mistakes, and confidence. Counterbalance task order where practical. Preserve qualitative feedback; a small convenience sample cannot establish general superiority.

## Proposed vertical slice

An existing HTTP transport; one handler; explicit active-work and waiting limits; body size/deadline limits; structured lifecycle measurements; graceful drain; one slow-handler demo. Prefer reuse of protocol and TLS implementations. No custom parser, Servlet compatibility, admin UI, or production release is needed for this learning milestone.

Acceptance criteria: limits behave as documented, cancellations release capacity, queue memory is bounded, and an external tester can explain the failure using the demo. Numerical performance targets should follow a baseline, not precede it.

## Results template

For each future run record: commit; environment; product/config versions; workload; offered rate; duration/warmup; raw-data location; correctness outcomes; latency/errors/resources; known limitations; conclusion. Until these fields contain measured evidence, all comparisons remain hypotheses.
