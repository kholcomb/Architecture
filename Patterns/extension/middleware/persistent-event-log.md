---
name: Persistent Event Log
category: extension/middleware
also-known-as: [Event Store, Commit Log, Immutable Log]
tags: [event-sourcing, append-only, replay, durability, streaming]
parent: middleware
related: [message-broker, event-mediator, enterprise-service-bus, middleware, shared-repository]
source: https://github.com/denyspoltorak/metapatterns/wiki/Middleware
---

## Summary
An append-only, ordered log of events that retains all events durably for a configurable retention period (or indefinitely). Consumers can read from any offset, enabling replay of historical events and bootstrapping new consumers with full history. Acts as the source of truth in event-sourced systems, replacing the shared database as the integration point between services.

## When To Use
- Consumers need to replay events from a specific point in time to rebuild state or recover from failure
- Multiple independent consumers need to process the same stream at their own pace without affecting each other
- The system requires an immutable audit trail of all state changes
- Event sourcing is used and the event log is the primary system of record

## When To Avoid
- Events are ephemeral and replay is never needed — a simple queue is sufficient and cheaper
- The volume of events makes long-term retention storage costs prohibitive without a clear benefit
- Consumers need random access to individual events rather than sequential stream processing
- The team lacks expertise in offset management, consumer group coordination, and schema evolution in log-based systems

## Pros and Cons

* Good, because consumers are fully decoupled from each other — each reads at its own pace from any offset
* Good, because complete event history enables time-travel debugging, audit trails, and rebuilding derived views
* Good, because new consumers can be added later and replay all historical events to build their own state
* Bad, because long retention of large event volumes requires significant storage and operational capacity
* Bad, because schema evolution is challenging — old events remain and must be compatible with new consumers
* Bad, because compaction, partitioning, and consumer lag management add operational complexity over simple queuing

## Evolutions
- **From:** Message Broker (add durable, replayable retention to basic message routing)
- **To:** Event Sourcing architecture (log as the canonical system of record), CQRS (separate read models rebuilt from the log), Data Lakehouse (replicate log to analytics storage)
