# Project brief

## Intent

Build a useful open-source infrastructure project in the broad space occupied by NGINX, Tomcat, and Netty. The goal is external adoption, supported by understandable architecture, reliable behavior, and contributor-friendly documentation.

## Proposed initial audience

Backend developers running small services who struggle to identify whether slow requests come from application execution, waiting for capacity, or slow clients. This pain is a hypothesis; no interviews have been conducted.

## Proposed promise

An HTTP runtime that makes request lifecycle and overload behavior easy to understand and control.

Example: when a handler slows down, an operator can see waiting time versus execution time, the active-request limit, and why additional work was rejected.

## Scope boundary

Choose one layer first. A reverse proxy, a servlet container, and a networking library have different users and compatibility obligations. Full compatibility with all three reference projects is outside the proposed first release.

Success means developers can explain an incident and run a small service reliably. Raw throughput alone is insufficient. We have no benchmark or adoption results yet.
