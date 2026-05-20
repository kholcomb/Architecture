---
name: Anticorruption Layer
category: extension/proxy
also-known-as: [ACL, Translation Layer, Integration Facade]
tags: [ddd, translation, isolation, legacy, domain-model]
parent: proxy
related: [adapter, facade, reverse-proxy, api-gateway, shared-repository, proxy]
source: https://github.com/denyspoltorak/metapatterns/wiki/Proxy
---

## Summary
A translation layer that insulates a clean domain model from a legacy or external system's messy, inconsistent, or semantically incompatible model. All communication between the internal system and the external system passes through the ACL, which translates concepts, data structures, and terminology in both directions — preventing the external model's corruption from spreading into the internal domain.

## When To Use
- Integrating with a legacy system whose data model or terminology would pollute the clean domain model if used directly
- A third-party API uses different concepts and naming conventions that do not map cleanly to internal domain language
- The external system's model is expected to change and those changes must be absorbed without cascading into the internal domain
- Bounded contexts in a domain-driven design must remain isolated from each other's models

## When To Avoid
- The external system's model is clean and compatible with the internal model — a simple adapter suffices
- The translation logic is trivial (field renaming only) and a full ACL layer adds unnecessary overhead
- Performance-sensitive paths cannot afford the overhead of translation on every interaction
- The external system is the authoritative source of truth and the internal model should intentionally mirror it

## Pros and Cons

* Good, because the internal domain model remains clean and expressed in the ubiquitous language of the domain
* Good, because changes to the external system are absorbed at the ACL boundary — the internal model is shielded
* Good, because the translation logic is isolated in one place, making it easy to test and evolve independently
* Bad, because adds overhead and complexity — every interaction requires translation in both directions
* Bad, because the ACL can become a large, complex component if the external system's model is very different
* Bad, because the translation mapping must be kept in sync as both systems evolve, requiring ongoing maintenance

## Evolutions
- **From:** Proxy (ACL is a semantics-translating proxy between incompatible domain models)
- **To:** Strangler Fig (progressively replace the legacy system while the ACL handles the transition period), Open Host Service (formalize the internal model's external interface as a published language)
