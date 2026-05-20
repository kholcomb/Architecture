---
name: Enterprise Service Bus
category: extension/middleware
also-known-as: [ESB, Integration Bus, Message-Oriented Middleware]
tags: [integration, transformation, orchestration, protocol-mediation, enterprise]
parent: middleware
related: [message-broker, event-mediator, middleware, api-gateway, anticorruption-layer]
source: https://github.com/denyspoltorak/metapatterns/wiki/Middleware
---

## Summary
A centralized middleware platform that provides message routing, data transformation, protocol mediation, and orchestration across enterprise systems. The ESB acts as a universal adapter and coordinator: it receives messages in various formats and protocols, transforms them to the target format, routes them to the correct system, and can orchestrate multi-step integration workflows. Evolved from the Middleware metapattern to address heterogeneous enterprise integration needs.

## When To Use
- Multiple systems with different protocols (SOAP, REST, FTP, EDI, proprietary) must communicate and the ESB handles translation
- Enterprise-wide integration requires a canonical data model that each system's data is mapped to and from
- Centralized monitoring, audit logging, and governance of all inter-system messages is required
- Legacy systems cannot be modified and need an adapter layer to participate in modern integrations

## When To Avoid
- New microservices architectures where lightweight message brokers or service meshes are more appropriate
- The ESB would become a bottleneck because all traffic must flow through it — consider decentralized alternatives
- Small-scale integrations where the configuration and operational overhead of an ESB is disproportionate
- The organization wants independent team autonomy — an ESB creates a shared platform that slows individual teams

## Pros and Cons

* Good, because a single platform handles transformation, routing, and protocol mediation across heterogeneous systems
* Good, because centralized monitoring and governance gives visibility into all enterprise data flows
* Good, because legacy systems can integrate through adapters without being modified
* Bad, because the ESB becomes a central point of failure and a deployment bottleneck affecting all integrated systems
* Bad, because ESB configurations accumulate complexity over time and become difficult to maintain or understand
* Bad, because performance overhead of transformation and routing can be significant for high-throughput scenarios

## Evolutions
- **From:** Message Broker (add transformation and orchestration capabilities), Event Mediator (scale up to enterprise-wide integration)
- **To:** Microservices with lightweight messaging (decompose ESB responsibilities to individual services), API Management Platform (expose ESB integrations as governed APIs)
