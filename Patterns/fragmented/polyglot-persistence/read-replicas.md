---
name: Read Replicas
category: fragmented/polyglot-persistence
also-known-as: [Read Replica, Secondary Replica, Follower]
tags: [replication, scalability, read-performance, high-availability, eventual-consistency]
parent: polyglot-persistence
related: [cache-aside, materialized-view, cqrs-view, polyglot-persistence]
source: https://github.com/denyspoltorak/metapatterns/wiki/Polyglot-Persistence
---

## Summary
Read Replicas are read-only copies of a primary database, kept in sync via continuous replication. All write operations target the primary; read queries are routed to one or more replicas to distribute read load and reduce contention on the primary. Replicas may lag slightly behind the primary, making data eventually consistent. This pattern is a simple and widely supported mechanism for scaling read throughput without sharding.

## When To Use
- The database is read-heavy and the primary is a bottleneck due to read query volume
- Reporting or analytics queries are long-running and should not compete with transactional queries on the primary
- Geographic distribution of replicas reduces read latency for users in distant regions
- High availability is required — replicas can be promoted to primary if the primary fails

## When To Avoid
- The workload is write-heavy; replicas only help with read scaling and do not reduce write load on the primary
- Strict read-your-writes consistency is required — replication lag means a write may not be visible on the replica immediately
- Replication lag is high enough that replicas serve significantly stale data for the use case's tolerance
- The overhead of managing replica infrastructure outweighs the read scaling benefit for low-traffic systems

## Pros and Cons

* Good, because read throughput scales horizontally by adding replicas without sharding or application changes
* Good, because long-running analytical queries on replicas do not impact transactional query performance on the primary
* Good, because replicas provide a warm standby for failover, improving availability
* Bad, because replication lag introduces eventual consistency — reads may not reflect the most recent writes
* Bad, because writes still target a single primary, so write throughput remains bounded by the primary's capacity
* Bad, because managing replica lag, monitoring replication health, and handling failover adds operational complexity

## Evolutions
- **From:** Single Primary Database (add replicas when read-heavy workloads saturate the primary)
- **To:** Sharding (scale write throughput by partitioning data across multiple primaries), CQRS View Database (go further by maintaining purpose-shaped projections rather than full replicas)
