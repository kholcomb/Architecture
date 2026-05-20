---
name: Data Lake
category: fragmented/polyglot-persistence
also-known-as: [Data Reservoir]
tags: [analytics, schema-on-read, raw-data, unstructured, exploratory]
parent: polyglot-persistence
related: [data-warehouse, materialized-view, event-sourcing, polyglot-persistence]
source: https://github.com/denyspoltorak/metapatterns/wiki/Polyglot-Persistence
---

## Summary
A Data Lake is a centralized repository that stores raw data in its native format — structured, semi-structured, or unstructured — without requiring a predefined schema at write time. Schema is applied on read, allowing diverse analytical workloads (machine learning, ad-hoc exploration, reporting) to interpret the same raw data differently. This approach defers the cost and rigidity of schema design, enabling storage of all data before its use cases are fully defined.

## When To Use
- Data needs to be ingested and retained before its analytical use cases are fully understood
- Multiple teams with different analytical needs (data science, BI, compliance) must access the same raw data in different shapes
- Unstructured or semi-structured data (logs, sensor streams, documents, media) must be stored alongside structured records
- Cost-effective long-term retention of high-volume raw data is a priority

## When To Avoid
- Structured, governed reporting with consistent schemas is the primary use case — a Data Warehouse is more appropriate
- The organization lacks the tooling and discipline to prevent the lake from becoming an unnavigable "data swamp"
- Consumers need low-latency, high-performance queries against well-defined schemas
- Data governance, lineage, and access control requirements cannot be met without a schema-on-write model

## Pros and Cons

* Good, because raw data is preserved in full fidelity — no information is lost to pre-transformation
* Good, because schema-on-read allows different consumers to interpret the same data differently without ETL for each use case
* Good, because storage costs are low for object/blob storage, making long-term retention economically feasible
* Bad, because without governance, the lake becomes a data swamp — data is present but undiscoverable and unreliable
* Bad, because schema-on-read queries are slower and require more compute than pre-transformed warehouse queries
* Bad, because data quality and consistency are the consumer's responsibility, increasing complexity for each analytical workload

## Evolutions
- **From:** Data Warehouse (augment with a lake for raw and unstructured data that doesn't fit the warehouse schema)
- **To:** Data Lakehouse (unify lake storage with warehouse-style table formats and ACID transactions), Feature Store (curate ML features from lake data for model training and serving)
