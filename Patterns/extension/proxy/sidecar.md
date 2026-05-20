---
name: Sidecar
category: extension/proxy
also-known-as: [Sidekick, Decomposed Container]
tags: [sidecar, co-deployment, cross-cutting, container, extensibility]
parent: proxy
related: [ambassador, service-mesh, api-gateway, proxy]
source: https://github.com/denyspoltorak/metapatterns/wiki/Proxy
---

## Summary
A helper container or process co-deployed alongside the main service that extends its capabilities — such as logging, configuration management, secret injection, or acting as a local proxy — without modifying the service code. The sidecar shares the same lifecycle and network namespace as the main service, enabling transparent augmentation of the service's behavior.

## When To Use
- Cross-cutting capabilities (logging agents, config watchers, secret injectors) must be added to a service without modifying its code
- The capability applies to many services regardless of their programming language or framework
- The helper and main service should scale and be deployed as a unit
- You want to isolate the operational concern from the application logic to maintain separation of responsibilities

## When To Avoid
- The overhead of running an extra process per service instance is too costly in resource-constrained environments
- The capability is simple enough to implement as an in-process library
- The team is not using a container orchestrator (Kubernetes, ECS) that natively supports co-deployment patterns
- Tight coupling between the sidecar and the main service would make independent updates difficult

## Pros and Cons

* Good, because cross-cutting concerns are isolated in a separate process — application code stays clean
* Good, because the sidecar is language-agnostic and can augment any service regardless of its tech stack
* Good, because the sidecar can be updated, replaced, or reused across many services independently
* Bad, because adds resource overhead — every service instance runs an additional process consuming CPU and memory
* Bad, because introduces inter-process communication complexity between the sidecar and the main service
* Bad, because debugging failures becomes harder because issues may originate in the sidecar rather than the application

## Evolutions
- **From:** Proxy (Sidecar is a co-located, per-instance specialization of the proxy concept)
- **To:** Service Mesh (compose many sidecars into a mesh with a unified control plane), Ambassador (specialize the sidecar as an outbound proxy)
