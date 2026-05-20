---
name: Service Layer
category: extension/orchestrator
also-known-as: [Application Service Layer, Use Case Layer]
tags: [application-layer, coordination, boundary, use-case, transactions]
parent: orchestrator
related: [facade, transaction-script, saga, api-composer, orchestrator]
source: https://github.com/denyspoltorak/metapatterns/wiki/Orchestrator
---

## Summary
A set of operations available to the application that defines the system's boundary and coordinates the application's response to each use case. The service layer acts as the orchestration layer above the domain model — it manages transactions, authorizes operations, coordinates between domain objects, and invokes infrastructure concerns (messaging, persistence, notifications). Business logic itself lives in the domain objects; the service layer only coordinates.

## When To Use
- The application has a rich domain model and needs a clear boundary that separates application coordination from domain logic
- Multiple client types (web, API, CLI) need to invoke the same use cases — the service layer provides a single reusable entry point
- Transactions and security checks must be applied consistently at the use-case level before any domain object is modified
- The domain model should not be exposed directly to callers — the service layer provides a stable API contract

## When To Avoid
- The application is simple and has no rich domain model — a transaction script is more appropriate
- The service layer duplicates what the domain objects could handle themselves, adding an unnecessary coordination layer
- The service layer accumulates business logic that should live in the domain, creating an anemic domain model
- A single, thin service per use case would just delegate to one domain method with no real coordination to perform

## Pros and Cons

* Good, because provides a clear, stable API boundary — clients are insulated from domain model changes
* Good, because transaction management, authorization, and cross-cutting orchestration are in one place
* Good, because multiple client types can invoke the same service layer operation, avoiding duplication of coordination logic
* Bad, because can become an anemic pass-through layer if business logic migrates from the domain into the service layer
* Bad, because adds another layer of abstraction that increases the number of classes and the depth of the call stack
* Bad, because boundaries between the service layer and domain model erode over time without disciplined enforcement

## Evolutions
- **From:** Orchestrator (Service Layer is a formal application-boundary orchestrator above the domain model)
- **To:** CQRS (split the service layer into separate command and query services), Hexagonal Architecture (formalize the service layer as the application port/use-case boundary)
