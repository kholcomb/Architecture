---
name: Service-Oriented Architecture
category: fragmented
also-known-as: []
tags: [soa, services, loose-coupling, interoperability, enterprise]
related: [layered-services, microservices, hierarchy, backends-for-frontends]
source: https://github.com/denyspoltorak/metapatterns/wiki/Service-Oriented-Architecture
---

## Summary
Service-Oriented Architecture (SOA) is an architectural style in which software components are published, discovered, and consumed as services. Services expose well-defined interfaces — historically via WSDL/SOAP over an Enterprise Service Bus (ESB), more recently via REST or messaging protocols — and are loosely coupled so that each can be developed, deployed, and versioned independently. SOA emphasizes reuse of shared services across multiple consumers and typically employs a centralized governance model to manage service contracts and lifecycle.

## When To Use
- The organization needs to integrate heterogeneous systems (legacy, packaged software, custom applications) under a unified service layer
- Business processes span multiple systems and need to be orchestrated or choreographed across organizational boundaries
- Enterprise-wide service reuse is a strategic priority and a governance model exists to enforce shared service contracts
- Long-lived, stable services serve multiple consumers that benefit from a well-governed, versioned contract

## When To Avoid
- The system is a single application with no integration requirements — SOA adds overhead with no benefit
- Teams are small and fast-moving; centralized ESB governance slows delivery
- Microservices with decentralized ownership are a better fit when services are small, independently scalable, and owned by autonomous teams
- Low-latency, high-throughput scenarios where ESB intermediaries introduce unacceptable overhead

## Pros and Cons

* Good, because heterogeneous systems are integrated through well-defined, technology-neutral service contracts
* Good, because shared services can be reused across consumers, reducing duplication of business logic
* Good, because services are loosely coupled — consumers depend on contracts, not implementations
* Bad, because centralized ESB or registry infrastructure becomes a single point of failure and a governance bottleneck
* Bad, because heavyweight WSDL/SOAP contracts and XML processing add significant overhead compared to lightweight alternatives
* Bad, because cross-service transactions and distributed coordination are complex and often require compensating transactions

## Evolutions
- **From:** Monolithic Application (extract capabilities into services to enable reuse and independent deployment)
- **To:** Microservices (decompose further into smaller, autonomously owned services with decentralized governance), Event-Driven Architecture (replace synchronous service calls with asynchronous messaging)
