---
name: Layers
category: basic
also-known-as: [Layered Architecture, Multitier Architecture, N-tier Architecture]
tags: [abstraction, separation-of-concerns, horizontal-tiers, specialization]
related: [monolith, services, hexagonal, pipeline]
source: https://github.com/denyspoltorak/metapatterns/wiki/Layers
---

## Summary
Organizes a system into horizontal tiers of abstraction — one component per level of abstractness. Each layer depends only on the layer below it, keeping business logic encapsulated and implementation details separate from higher-level concerns. The guiding principle: "Don't mix the business logic and implementation details." It is the natural first step for adding structure to a monolith, and the dominant pattern for small-to-medium codebases.

## When To Use
- The project is small to medium in size (below ~100,000 lines of code)
- Teams can specialize by layer (e.g., a dedicated data-access team, a UI team)
- Components need to be deployed to dedicated hardware tiers
- Independent scaling of layers is required
- Real-time or embedded systems need clear separation between hardware and logic

## When To Avoid
- The project is large or growing toward 1,000,000+ lines of code — the pattern deteriorates under that scale
- More than a few teams need to work independently without force conflicts across subdomains
- Low-latency decision-making requires real-time application of business logic without passing through abstraction tiers

## Pros and Cons

* Good, because development can start quickly with a familiar, well-understood structure
* Good, because debugging is straightforward — issues are isolated to a single layer
* Good, because teams can specialize per layer, reducing cognitive overhead
* Good, because business logic is encapsulated and separated from infrastructure concerns
* Good, because layers without business logic (e.g., data access) are reusable across features
* Good, because layers can be deployed to dedicated hardware for independent scaling
* Bad, because the structure deteriorates rapidly as the project grows beyond medium scale
* Bad, because large teams hit force conflicts across subdomains that layers cannot resolve
* Bad, because aggressive cross-layer optimizations are difficult to apply cleanly

## Evolutions
- **From:** Monolith (add internal structure without splitting deployments)
- **To:** Services (split subdomains into independently deployable units), Hexagonal Architecture (invert dependencies to isolate the domain), add Caching/Batching/Aggregation layers for performance, Plugins for extensibility
