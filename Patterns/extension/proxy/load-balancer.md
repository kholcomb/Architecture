---
name: Load Balancer
category: extension/proxy
also-known-as: [Traffic Distributor, Layer 4/7 Balancer]
tags: [scalability, availability, distribution, failover, traffic]
parent: proxy
related: [reverse-proxy, api-gateway, service-mesh, edge-service, proxy]
source: https://github.com/denyspoltorak/metapatterns/wiki/Proxy
---

## Summary
A proxy that distributes incoming requests across a pool of backend instances using a configured algorithm (round-robin, least-connections, IP hash, etc.). Ensures no single instance is overwhelmed, provides automatic failover when instances become unavailable, and enables horizontal scaling by adding or removing instances from the pool transparently.

## When To Use
- A service must handle more traffic than a single instance can serve and horizontal scaling is required
- High availability is required — if one instance fails, traffic must be automatically redirected to healthy instances
- Backend instances need to be added or removed from the pool without client-visible disruption
- Traffic distribution across geographically distributed instances or availability zones is needed

## When To Avoid
- A single backend instance is sufficient — the load balancer adds overhead without benefit
- Stateful sessions require all requests from a client to reach the same instance and sticky sessions are not an option
- The load balancer itself would become an unmitigated single point of failure in a zero-downtime requirement
- Service mesh sidecar load balancing already handles distribution at the client side, making an external load balancer redundant

## Pros and Cons

* Good, because distributes traffic across instances, enabling horizontal scaling beyond a single machine's capacity
* Good, because health checks detect and remove failed instances from the pool automatically, improving availability
* Good, because backend pool changes (scale out, deployments, replacements) are invisible to clients
* Bad, because the load balancer itself is a potential single point of failure and requires its own high-availability setup
* Bad, because stateful applications with session affinity requirements add complexity to load balancing configuration
* Bad, because adds a network hop to every request, increasing latency and introducing another component to monitor

## Evolutions
- **From:** Proxy (Load Balancer is a proxy specialized for distributing traffic across a pool of backends)
- **To:** Service Mesh (distribute load balancing to client-side sidecar proxies for finer-grained control), API Gateway (add application-layer routing and cross-cutting concerns on top of load balancing)
