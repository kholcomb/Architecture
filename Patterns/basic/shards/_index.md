---
name: Shards
category: basic
also-known-as: [Instances, Replicas]
tags: [scalability, replication, stateless, fault-tolerance, horizontal-scaling]
related: [monolith, services, pipeline]
source: https://github.com/denyspoltorak/metapatterns/wiki/Shards
---

## Summary
Multiple functionally identical subsystems with little or no intercommunication. Known as "Attack of the clones," the Shards pattern solves scalability by running parallel replicas of the same component — as stateless pools, persistent copies, geographic instances, or per-session actors. Performance is optimal when requests stay within a single shard; it degrades sharply when shards must synchronize shared state.

## When To Use
- Load is high or variable and exceeds the capacity of a single server
- Redundancy is needed to survive hardware failures
- Worst-case latency must be reduced by allowing parallel replica responses
- Geographic locality requires deploying instances close to users
- A canary release strategy is required to roll out changes progressively

## When To Avoid
- Multiple instances must modify the same dataset — write conflicts and distributed transactions erode both consistency and performance
- The system's core logic is inherently stateful and cannot be partitioned cleanly

## Pros and Cons

* Good, because horizontal scaling is straightforward — add more identical instances
* Good, because replica redundancy improves fault tolerance and availability
* Good, because geographic distribution reduces latency for regional users
* Good, because stateless shards can be reset and redeployed independently
* Bad, because shared mutable state requires complex synchronization or distributed transactions
* Bad, because deploying or updating multiple components increases operational effort
* Bad, because write conflicts can damage data consistency when shards share a dataset

## Evolutions
- **From:** Monolith or Services (when a single instance can no longer handle load)
- **To:** Shared Repository (move shared data out of shards), Space-Based Architecture (tolerate write collisions), Sharding Proxy or Orchestrator (hide shard topology from callers), Middleware (enable inter-shard communication)
