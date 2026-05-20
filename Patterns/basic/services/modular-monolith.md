---
name: Modular Monolith
category: basic/services
also-known-as: [Structured Monolith, Majestic Monolith]
tags: [monolith, modules, encapsulation, single-deployable, explicit-api, enforced-boundaries]
parent: services
related: [layered-monolith, microservices, service-based-architecture, domain-driven-design]
source: https://github.com/denyspoltorak/metapatterns/wiki/Services
---

## Summary
A single-deployable application partitioned into well-defined modules that expose explicit public APIs while hiding internal implementation. Module boundaries are enforced by packaging rules, access modifiers, build tooling, or architectural fitness functions — not merely by naming convention. Each module is conceptually independent and could, in principle, be extracted into a separate service; it simply has not been because the operational cost of doing so is not yet justified.

## When To Use
- A single deployment unit is operationally appropriate but internal structure must prevent the codebase from becoming a Big Ball of Mud
- The team wants the option to migrate to microservices later without rewriting — enforced module boundaries make extraction safer
- Domain boundaries are still being discovered — working in a single codebase is faster to refactor than distributed services
- Operational simplicity (single process, single database, simple CI/CD) is a priority

## When To Avoid
- Individual modules have drastically different scaling or resource requirements that demand independent deployment
- Teams need autonomous release cycles that are blocked by a shared deployment pipeline
- The domain is already well-understood and stable enough that the extraction cost to microservices is justified by team autonomy

## Pros and Cons

* Good, because module boundaries are enforced by tooling, making architectural erosion detectable at build or test time
* Good, because in-process calls remain fast and avoid the distributed systems tax of network latency and serialization
* Good, because the single deployment pipeline keeps operational complexity low while the product matures
* Bad, because all modules must be deployed together — a bug in one module still requires redeploying the entire application
* Bad, because shared infrastructure (database, runtime) means one misbehaving module can impact all others
* Bad, because enforced module isolation requires tooling investment (ArchUnit, Dependency Cruiser, package-private access rules) that many teams skip

## Evolutions
- **From:** Layered Monolith (add enforced module boundaries alongside existing layer boundaries)
- **To:** Service-Based Architecture (extract the most change-heavy modules into independently deployable services), Microservices (extract all modules into fine-grained services once domain boundaries and operational maturity warrant it)
