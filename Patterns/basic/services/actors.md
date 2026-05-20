---
name: Actors
category: basic/services
also-known-as: [Actor Model, Actor-Based Services, Virtual Actors]
tags: [async, message-passing, isolation, concurrency, no-shared-state, distributed]
parent: services
related: [microservices, faas, event-driven-architecture, saga]
source: https://github.com/denyspoltorak/metapatterns/wiki/Services
---

## Summary
Each service (or fine-grained unit of logic) is modeled as an actor: an independent entity with its own private state and a message inbox. Actors communicate exclusively by sending asynchronous messages to each other's inboxes — there are no direct method calls, no shared memory, and no shared mutable state between actors. An actor processes one message at a time, which eliminates concurrency bugs within a single actor. The model scales naturally across cores and nodes because message passing is location-transparent.

## When To Use
- High concurrency is required and shared-state synchronization (locks, transactions) is a bottleneck or complexity source
- Services must communicate asynchronously with natural backpressure through bounded mailboxes
- The system needs fine-grained fault isolation — a crashed actor can be supervised and restarted without affecting others
- Location transparency is valuable — actors can be co-located or distributed across nodes without changing call semantics

## When To Avoid
- The team is unfamiliar with asynchronous message-passing semantics — debugging mailbox starvation and deadlocks requires different mental models
- Strong transactional consistency is required across multiple actors — coordination across isolated state is complex
- Request/response latency must be minimal and predictable — async message round-trips add overhead versus direct calls

## Pros and Cons

* Good, because actors process messages sequentially, eliminating within-actor race conditions without explicit locking
* Good, because supervision hierarchies allow automatic fault recovery — a failed actor is restarted by its supervisor
* Good, because location transparency makes it straightforward to move actors across nodes for elasticity
* Bad, because async message-passing makes request tracing, debugging, and reasoning about ordering harder than synchronous calls
* Bad, because coordinating a transaction across multiple actors requires explicit protocols (Saga, two-phase commit via messages) rather than ACID transactions
* Bad, because mailbox overflow and dead-letter handling must be explicitly designed, or messages are silently lost

## Evolutions
- **From:** Microservices (adopt actor model within or across services for high-concurrency coordination and fault isolation)
- **To:** Virtual Actors / Grains (managed actor lifecycle by a platform like Orleans or Dapr Actors), Event Sourcing (persist the stream of messages processed by each actor as its state history)
