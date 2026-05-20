---
name: API Gateway
category: extension/proxy
also-known-as: [Edge Gateway, API Front Door]
tags: [routing, auth, rate-limiting, ingress, aggregation]
parent: proxy
related: [load-balancer, reverse-proxy, ambassador, sidecar, backends-for-frontends, api-composer]
source: https://github.com/denyspoltorak/metapatterns/wiki/Proxy
---

## Summary
A single-entry-point proxy in front of backend services that handles cross-cutting concerns — authentication, rate limiting, routing, SSL termination, and request/response transformation — on behalf of all clients. Backend topology is invisible to clients.

## When To Use
- Multiple clients (web, mobile, third-party) need different auth or format requirements from the same backend
- Cross-cutting concerns (auth, rate limiting, logging) should not be duplicated across services
- Backend service topology must evolve without breaking client contracts
- A single stable external endpoint is required (DNS, certificates, firewall rules)

## When To Avoid
- A single backend service — the gateway adds pure overhead
- The gateway would become a bottleneck or single point of failure without a viable bypass
- Business logic accumulates inside the gateway — consider a BFF or Orchestrator instead
- The team lacks capacity to operate and maintain the gateway infrastructure at high availability

## Pros and Cons

* Good, because cross-cutting concerns are centralized — backend services stay thin
* Good, because backend topology changes without clients noticing
* Good, because a single ingress point simplifies firewall rules, certificates, and monitoring
* Bad, because a single point of failure — requires high-availability deployment
* Bad, because adds a network hop and latency to every request
* Bad, because gateway configuration accumulates complexity — routing rules, auth policies, transformations

## Evolutions
- **From:** Proxy (API Gateway is a specialized full-proxy with application-layer awareness)
- **To:** BFF (per-client gateway instances), API Composer (add response aggregation logic), Service Mesh (move per-service traffic policy out of the gateway)
