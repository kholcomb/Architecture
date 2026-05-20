---
name: Data Mesh
category: basic/pipeline
also-known-as: [Federated Data Architecture, Domain-Oriented Data Ownership]
tags: [data-products, domain-ownership, federated-governance, decentralization, self-serve, analytical-data]
parent: pipeline
related: [event-driven-architecture, stream-processing, batch-processing, microservices]
source: https://github.com/denyspoltorak/metapatterns/wiki/Pipeline
---

## Summary
Decentralizes data ownership by assigning each domain team responsibility for publishing its data as a versioned, discoverable, and interoperable data product. A federated governance layer — shared standards for schema, quality SLAs, and access control — ensures that data products across domains remain composable without requiring a central data team to own or transform all data. Contrasts with centralized data lakes and warehouses, where a single platform team becomes the bottleneck for every analytical use case.

## When To Use
- Multiple domain teams produce data that other teams need for analytics or ML, and a central data team cannot keep up with demand
- Data quality and freshness problems are caused by the distance between data producers and the central pipeline that transforms their data
- The organization is large enough that federated ownership reduces bottlenecks more than it introduces coordination overhead
- Domain teams already have strong ownership culture and the tooling maturity to publish and maintain data products

## When To Avoid
- The organization is small — a central data warehouse or lake is simpler to operate and reason about
- Domain teams lack the engineering capacity or maturity to own data quality and SLA obligations on top of their operational systems
- Data integration patterns are highly complex and require centralized transformation expertise that domain teams do not possess
- Federated governance tooling (data catalog, schema registry, lineage tracking) is not available or too immature to enforce standards

## Pros and Cons

* Good, because domain teams who produce data are closest to it and can ensure quality and freshness better than a central team
* Good, because removing the central data team bottleneck enables parallel development of analytical capabilities across domains
* Good, because versioned data products give consumers explicit contracts and allow producers to evolve independently
* Bad, because federated governance requires significant organizational discipline — without it, data products become inconsistent and undiscoverable
* Bad, because duplicating data pipeline tooling across many domain teams increases infrastructure cost compared to a shared centralized platform
* Bad, because discoverability and lineage across many independently published products requires a mature data catalog investment

## Evolutions
- **From:** Centralized Data Lake or Data Warehouse (distribute ownership to domain teams when central pipeline becomes a bottleneck)
- **To:** Event-Driven Architecture (stream domain events directly as real-time data products), Data Lakehouse (combine centralized storage with federated access patterns)
