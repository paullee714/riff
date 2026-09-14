# Candidate concepts

All assessments below are our design judgments, not measured market findings.

| Concept | Primary user and value | Main difficulty | First experiment |
| --- | --- | --- | --- |
| A. Observable HTTP runtime | Backend developers: explicit limits, lifecycle timing, and overload explanations | Distinguishing it from existing servers plus telemetry | Reproduce a slow-handler incident and compare diagnosis |
| B. Small reverse proxy | Operators of a few services: understandable routing and failure behavior | Mature competition and security-sensitive protocol handling | Compare configuring and diagnosing one route against NGINX/Caddy |
| C. Protocol server toolkit | Developers of custom TCP protocols: approachable pipeline and lifecycle APIs | Buffer ownership, backpressure, cancellation, and ecosystem adoption | Implement the same framed protocol with Netty and a proposed API |
| D. Minimal application container | JVM users: simple application loading and operations | Servlet compatibility and lifecycle scope can expand quickly | Interview teams about a concrete missing deployment capability |

## Recommendation to investigate

Start with A, subject to interviews. Its narrow promise can be demonstrated by one incident walkthrough. First try it as a thin layer on an existing HTTP transport; a useful library may emerge without replacing low-level networking.

## Language remains open

- JVM: investigate if Netty users are the target and existing Java/Kotlin experience reduces delivery risk.
- Rust: investigate for native deployment and explicit resource ownership; account for implementation and API complexity.
- Go: investigate for a small deployable service with straightforward operations.

Choose from maintainer experience and a short prototype, not hypothetical benchmark superiority. Building directly on operating-system event APIs is a separate learning path with a much larger correctness burden.
