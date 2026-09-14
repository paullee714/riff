# Market and product opportunities

Date: 2026-09-15. This is qualitative desk research and product inference, not a market-size estimate or proof of demand.

## Competitive implication

The [feature comparison](01-product-feature-comparison.md) shows capable incumbents across web serving, application hosting, and networking. Our inference: a new general-purpose replacement has a large trust and migration burden. A smaller tool that improves an existing deployment is a more testable entry point.

## Candidate segments

| Segment hypothesis | Job to accomplish | Adoption obstacle | Useful discovery evidence |
| --- | --- | --- | --- |
| Small backend teams | Diagnose slow or overloaded services without a large operations stack | Existing server plus metrics may already suffice | Recent incident, tools used, time spent finding cause |
| JVM library authors | Compose protocol handlers with understandable execution and resource limits | Netty familiarity and integration cost | Repeated custom glue code across projects |
| Operators of a few services | Configure routes and recover from failures easily | Mature proxy choices and production risk | A specific failure that current config/logs made difficult |
| Systems learners | Understand event loops and backpressure | Learning interest may not become production adoption | Ability to reproduce and explain a failure scenario |

These are possible audiences, not surveyed customer groups. Learning value and production demand should be measured separately.

## Three product bets

1. **Riff Runtime:** embeddable HTTP runtime with a small API and explicit execution/resource policies. Best fit for the current framework identity. Risk: becoming a thin wrapper without enough value.
2. **Riff Inspect:** diagnostics and reproducible overload scenarios integrated with an existing transport. Fastest way to test whether explanations matter. Risk: existing telemetry solves the same problem.
3. **Riff Proxy:** standalone proxy emphasizing comprehensible failure behavior. Easy demo, but competes directly with mature operational tooling.

Proposed sequence: investigate Runtime through an Inspect-style demo. Keep Proxy as an alternative until interviews establish the deployment layer. No language or architecture is committed.

## Proposed differentiator

“Understand why a request waited, failed, or was rejected.”

A useful demo would show an intentionally slow handler, the occupied capacity, queue wait, and resulting rejection with one documented configuration. Compare this against a baseline configured competently with its existing metrics and logs. If a small documentation or integration package solves the problem, that may be the better open-source contribution.

## Open-source adoption plan

Start with a runnable example, a precise limitations statement, and a reproducible incident tutorial. Invite users to try it in local or staging environments. Track successful independent setup and repeated use, not only stars or downloads. Before a production release, establish supported versions, security reporting, release notes, and maintenance expectations.

Potential future business models include support or hosted diagnostics, but neither is selected. Early adoption research should ask about integration effort and maintenance ownership before pricing.

## Discovery backlog

Interview 5–8 developers from one chosen segment. Ask about the last real failure, current stack, diagnosis steps, and what they tried. Do not lead with a list of Riff features. With permission, use sanitized reproductions; avoid collecting production payloads.

Proposed next-stage gate: three independently reported recurring pains and two volunteers willing to try the incident demo. Stop or redirect if existing configuration solves all observed cases or users will not introduce another dependency. This gate is a planning heuristic, not a statistically representative result.

Market size, geographic demand, willingness to pay, deployment share, and package adoption have not been measured. Avoid inferring a market size from GitHub popularity or public web-server fingerprints, which cannot represent embedded libraries consistently.
