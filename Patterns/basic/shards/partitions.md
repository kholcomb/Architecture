---
name: Partitions
category: basic/shards
also-known-as: [Horizontal Sharding, Range Sharding, Hash Sharding, Data Sharding]
tags: [data-sharding, scalability, key-range, distributed-data, horizontal-partitioning]
parent: shards
related: [cells, stateless-pool, multitenancy, consistent-hashing]
source: https://github.com/denyspoltorak/metapatterns/wiki/Shards
---

## Summary
Data is divided into non-overlapping horizontal slices distributed across multiple nodes. Each partition owns an exclusive key range (or a hash bucket) and is the sole authority for reads and writes on those keys. Queries are routed to the owning partition, enabling the dataset and request throughput to grow linearly by adding more nodes.

## When To Use
- A single node cannot hold the full dataset or cannot serve the write throughput required
- Access patterns are well-understood and a high-cardinality partition key distributes load evenly
- Queries are almost always scoped to a single partition key — most reads and writes touch one shard
- Linear data growth is expected and re-partitioning (or consistent hashing) is operationally feasible

## When To Avoid
- Queries frequently span multiple partitions — scatter-gather adds latency and coordination cost
- The partition key has low cardinality or skewed distribution, causing hot partitions
- Cross-partition transactions are required; distributed transactions are expensive and fragile
- The dataset is small enough that a single node with replicas handles the load more simply

## Pros and Cons

* Good, because storage and write throughput scale horizontally by adding partitions without full-table migrations
* Good, because each partition is a smaller, faster dataset — index scans and cache hit rates improve per node
* Good, because partition-local failures affect only the data range of that shard, bounding impact
* Bad, because cross-partition queries require scatter-gather or a secondary index, adding latency and complexity
* Bad, because uneven key distributions create hot spots that negate the scaling benefit
* Bad, because rebalancing partitions when adding or removing nodes requires data movement and careful coordination to avoid downtime

## Evolutions
- **From:** Shards (Partitions are the canonical data-layer application of the shard concept)
- **To:** Cells (promote partition to a full-stack boundary), Consistent Hashing (minimizes data movement during rebalancing), or Columnar Partitioning (partition by column groups for analytical workloads)
