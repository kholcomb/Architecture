---
name: Batch Processing
category: basic/pipeline
also-known-as: [Bulk Processing, Scheduled Jobs, ETL]
tags: [batch, scheduled, high-throughput, etl, offline, periodic, bounded-data]
parent: pipeline
related: [stream-processing, pipes-and-filters, workflow-system, data-mesh]
source: https://github.com/denyspoltorak/metapatterns/wiki/Pipeline
---

## Summary
Data is accumulated over a time interval and then processed as a discrete, bounded job. Jobs are typically scheduled (hourly, nightly, weekly) and operate on a complete snapshot or incremental slice of data. Batch processing is optimized for high throughput rather than low latency: large volumes of records are processed efficiently using sequential I/O, bulk operations, and distributed parallelism. It is the foundational pattern for ETL pipelines, periodic reporting, and bulk data transformations.

## When To Use
- Results are only needed periodically and latency of minutes to hours is acceptable
- Processing requires access to a complete or consistent snapshot of a dataset that is only available at a boundary
- High throughput at low cost is more important than real-time results — batch jobs amortize startup cost over large datasets
- Historical reprocessing or backfill is required — batch jobs can be re-run against past data with known-good logic

## When To Avoid
- Business processes require real-time or near-real-time results — batch latency introduces unacceptable delay
- The incoming data rate is too high to accumulate economically before processing
- Failures mid-job require partial retry capability that the batch framework does not natively support

## Pros and Cons

* Good, because simpler to develop, test, and reason about than streaming — data is bounded and jobs are deterministic
* Good, because high throughput at low cost — bulk I/O and columnar processing are well-optimized for large datasets
* Good, because jobs are independently rerunnable — a failed or incorrect job can be corrected and replayed against past data
* Bad, because introduces latency equal to the batch interval — results are stale between runs
* Bad, because large jobs accumulate failures silently until the end, and partial failure recovery can be complex
* Bad, because resource usage is spiky — large batch windows cause periodic peaks in compute and I/O demand

## Evolutions
- **From:** Ad-hoc scripts or manual exports (formalize into scheduled, observable batch pipelines)
- **To:** Stream Processing (reduce latency by shifting from periodic jobs to continuous processing), Workflow System (add dependency management, retries, and human approval steps between batch stages)
