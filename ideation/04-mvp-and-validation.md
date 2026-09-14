# Proposed MVP and validation

This plan assumes concept A. It is a proposal, with no implementation or completed experiments.

## Smallest useful behavior

1. Start an HTTP/1.1 service with one handler and a documented configuration.
2. Set request-body, active-request, queue, and timeout limits with explicit units and defaults.
3. Report request count, errors, active work, queue wait, and handler duration; distinguish timeouts from capacity rejection.
4. Shut down by stopping admission and draining work to a configured deadline.
5. Include a slow-handler example with a reproducible explanation of the observed failure.

Reuse a mature HTTP parser and TLS implementation. Keep diagnostic endpoints disabled or loopback-only by default, and avoid recording request bodies or credentials. The initial prototype can run locally behind an established TLS proxy.

Defer custom protocols, servlet compatibility, HTTP/3, distributed configuration, an admin GUI, a plugin marketplace, and automatic retries. Retry behavior requires separate semantics, especially for non-idempotent requests.

## Proposed validation gates

- Interview five backend developers: ask for their last latency or overload incident, current tools, diagnostic steps, and willingness to try a prototype. Record evidence before presenting the concept.
- Continue toward an MVP if at least three describe a recurring relevant problem and two agree to test. These are decision thresholds, not research findings.
- Compare an existing server with ordinary telemetry against the prototype using the same workload. If the advantage is configuration or documentation, consider publishing that integration instead.

## Engineering experiment

Use fast handlers, slow handlers, slow readers, aborted clients, and overload. Check bounded memory/queues, timeout behavior, graceful shutdown, and malformed-request handling. Add meaningful tests for these behaviors once code exists.

Measure throughput, p50/p95/p99 latency, error/rejection rates, CPU, and memory. Publish hardware, OS, runtime versions, load-generator settings, connection/TLS settings, limits, warmup, repetitions, and raw results. Separate time waiting from time executing. Check that the load generator is not the bottleneck and account for coordinated omission. No performance claim is justified before this experiment.

## First milestones

1. Validate audience and pain; select one concept and language.
2. Draft public API/configuration examples and an incident walkthrough.
3. Build one vertical slice and run correctness experiments.
4. Ask two external developers to reproduce the walkthrough without assistance.
5. Prepare a release with installation docs, contributor guidance, and a security reporting route.
