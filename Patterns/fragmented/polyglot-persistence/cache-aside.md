---
name: Cache-Aside
category: fragmented/polyglot-persistence
also-known-as: [Lazy Loading Cache]
tags: [caching, lazy-loading, read-performance, resilience]
parent: polyglot-persistence
related: [read-replicas, materialized-view, cqrs-view, polyglot-persistence]
source: https://github.com/denyspoltorak/metapatterns/wiki/Polyglot-Persistence
---

## Summary
Application code checks the cache first before reading from the database. On a cache miss, the application loads the value from the primary datastore, stores it in the cache, and returns it to the caller. The cache is not the system of record — it is a lazy-loaded, potentially expiring copy. Writes go directly to the primary store and may invalidate or update the cache entry.

## When To Use
- Read-heavy workloads where the same data is fetched repeatedly and changes infrequently
- The primary datastore is expensive to query (latency, throughput cost) and a fast cache layer is available
- Cache population from a warm-up process is impractical or unnecessary — lazy loading on first miss is acceptable
- Application logic can tolerate briefly stale data during the TTL window

## When To Avoid
- Write-heavy workloads where cache entries are invalidated so frequently the cache provides no benefit
- Data changes require strict read-your-writes consistency immediately after a mutation
- The cost of a cache miss (cold start storm at startup) is unacceptable under high concurrency
- Cache invalidation logic is complex enough that maintaining correctness outweighs the performance gain

## Pros and Cons

* Good, because only requested data is cached — the cache is populated on demand without pre-warming overhead
* Good, because cache failures are non-fatal; the application falls back to the primary store transparently
* Good, because TTL-based expiry provides a simple correctness bound without complex invalidation logic
* Bad, because the first request for any item always incurs the full primary-store latency (cache miss penalty)
* Bad, because stale data can be served until the TTL expires or an explicit invalidation occurs
* Bad, because thundering herd — many simultaneous misses for the same key can overwhelm the primary store

## Evolutions
- **From:** Direct Database Reads (introduce cache-aside when read latency or database load becomes a bottleneck)
- **To:** Read-Through Cache (move cache population logic into the cache layer itself), Materialized View (pre-compute and persist query results rather than caching raw rows)
