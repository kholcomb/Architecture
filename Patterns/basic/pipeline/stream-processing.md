---
name: Stream Processing
category: basic/pipeline
also-known-as: [Real-Time Processing, Continuous Processing, Event Stream Processing]
tags: [real-time, streaming, low-latency, stateful, unbounded-data, continuous-computation]
parent: pipeline
related: [event-driven-architecture, batch-processing, pipes-and-filters, data-mesh]
source: https://github.com/denyspoltorak/metapatterns/wiki/Pipeline
---

## Summary
Data is processed continuously as it arrives on an unbounded stream, with results produced in near real-time rather than after a full dataset is accumulated. Processing topologies transform, filter, aggregate, and join events in flight. Stateful computations (windowed aggregations, session tracking) maintain state in a distributed store that is checkpointed for fault tolerance. Stream processing enables per-event reactions and low-latency analytics on data that is never fully at rest.

## When To Use
- Business decisions must react to events within seconds or milliseconds — batch latency is unacceptable
- Continuous monitoring, alerting, or real-time dashboards require up-to-the-moment computation results
- Data volumes are too high to store first and process later without incurring prohibitive storage cost or latency
- The system needs to join or correlate events from multiple streams over time windows

## When To Avoid
- Latency requirements are loose — batch processing is simpler to develop, test, and operate
- The computation requires a complete, bounded dataset (e.g., full historical aggregations) that is not available until a batch boundary
- The team lacks experience with stateful stream processing — windowing semantics, watermarks, and exactly-once delivery guarantees have steep learning curves
- Operational complexity of a streaming platform (Kafka, Flink, Spark Streaming) is not justified by the latency requirements

## Pros and Cons

* Good, because results are produced with low latency — reacting to events within milliseconds is possible
* Good, because processing occurs in flight, reducing the need to store raw data before transformation
* Good, because horizontal scaling of stateless and stateful operators allows throughput to grow with data volume
* Bad, because exactly-once semantics and stateful recovery require careful platform configuration and add operational complexity
* Bad, because debugging and testing stream topologies — especially windowed and late-arriving event handling — is significantly harder than batch jobs
* Bad, because streaming infrastructure (brokers, distributed state stores) has higher baseline operational overhead than batch schedulers

## Evolutions
- **From:** Batch Processing (reduce latency by moving from periodic jobs to continuous event-by-event processing)
- **To:** Data Mesh (publish stream outputs as versioned data products consumed by other domains), Lambda Architecture (combine streaming for real-time results with batch for historical reprocessing)
