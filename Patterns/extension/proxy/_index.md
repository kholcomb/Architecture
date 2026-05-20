---
name: Proxy
category: extension
also-known-as: [Intermediary, Gateway, Facade]
tags: [proxy, routing, cross-cutting, interception, transparency]
related: [api-gateway, sidecar, ambassador, load-balancer, reverse-proxy, edge-service, anticorruption-layer, caching-layer, presentation-layer, adapter]
source: https://github.com/denyspoltorak/metapatterns/wiki/Proxy
---

## Summary
An intermediary that sits between a client and a component, forwarding requests and optionally adding cross-cutting behavior such as routing, caching, transformation, authentication, or observability. The proxy is typically transparent to one or both sides — the client sees only the proxy, not the downstream component, and the downstream component may be unaware of the proxy.

## When To Use
- Cross-cutting concerns (auth, logging, retries, caching) must be applied without modifying the target component
- The real component's location or identity needs to be hidden from the client
- You need to intercept, inspect, or transform requests before they reach the target
- A stable contract toward the client must be maintained while the implementation can vary behind the proxy

## When To Avoid
- The cross-cutting concern is simple enough to be handled inline without the indirection overhead
- Latency introduced by the proxy hop is unacceptable for the use case
- The proxy would accumulate business logic — a dedicated orchestrator or service is more appropriate
- The added operational complexity of maintaining the proxy outweighs its benefits in small deployments

## Pros and Cons

* Good, because cross-cutting concerns are isolated in one place and don't pollute application code
* Good, because the client is shielded from changes to the target component's location or interface
* Good, because behavior can be added or modified (caching, retries, security) without touching either client or target
* Bad, because introduces an additional network or function call hop, increasing latency
* Bad, because the proxy becomes a shared failure domain — a bug or outage affects all callers
* Bad, because complex proxy logic is hard to debug because it sits outside the normal application flow

## Evolutions
- **From:** Direct client-to-component calls (introduce proxy to add cross-cutting behavior)
- **To:** API Gateway (application-layer, multi-client proxy), Service Mesh (per-service sidecar proxies), Reverse Proxy (infrastructure-level), Anticorruption Layer (semantic translation)
