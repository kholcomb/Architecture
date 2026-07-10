---
name: Edge Service
description: Proxy at the network edge (CDN PoP near users) serving content with minimal latency by avoiding origin round-trips
category: extension/proxy
also-known-as: [CDN Edge, Point of Presence, Edge Node]
tags: [cdn, edge, latency, geographic, offloading]
parent: proxy
related: [reverse-proxy, caching-layer, load-balancer, api-gateway, proxy]
source: https://github.com/denyspoltorak/metapatterns/wiki/Proxy
---

## Diagram

```mermaid
graph LR
    U[User] --> E[Edge / PoP]
    E -->|cache hit| U
    E -->|cache miss| OR[Origin]
```

## Summary
A proxy deployed at the network edge — within a CDN point of presence (PoP) geographically close to users — that serves content with minimal latency by avoiding a round-trip to the origin. Handles TLS termination, static asset caching, DDoS protection, and routing at the edge. Dynamic requests can be forwarded to the nearest origin, while static or cacheable responses are served directly from the edge node.

## When To Use
- Users are geographically distributed and origin round-trip latency is unacceptable for the use case
- Static assets (JavaScript, CSS, images, video) represent the majority of traffic and can be cached at the edge
- DDoS protection, bot detection, or WAF rules must be applied before traffic reaches the origin
- TLS termination and HTTP/2 or HTTP/3 upgrades should be handled close to users to minimize handshake overhead

## When To Avoid
- All users are in a single geographic region and the origin is already close to them
- Content is highly dynamic and personalized, resulting in very low cache hit rates at the edge
- Regulatory data residency requirements prevent content from being stored or processed in certain jurisdictions where edge nodes operate
- The additional cost of CDN edge services is not justified by the performance improvement for the traffic volume

## Pros and Cons

* Good, because dramatically reduces latency for geographically distributed users by serving content from nearby PoPs
* Good, because static content served from the edge offloads significant bandwidth and compute from origin servers
* Good, because DDoS attacks and malicious traffic are absorbed at the edge before reaching origin infrastructure
* Bad, because edge cache invalidation is slower and more complex than local cache invalidation — stale content may persist briefly across PoPs
* Bad, because dynamic, uncacheable content still round-trips to the origin, limiting edge benefit for highly personalized apps
* Bad, because CDN vendors lock-in concerns arise — edge logic (workers, functions) may use proprietary APIs

## Evolutions
- **From:** Reverse Proxy (push the proxy to the CDN edge for geographic distribution)
- **To:** Edge Computing (run business logic at the edge, not just routing/caching), Multi-CDN (distribute across multiple edge providers for resilience)
