---
name: ML Systems
category: ai
also-known-as: [MLOps Patterns, Machine Learning Infrastructure Patterns]
tags: [mlops, training, inference, feature-engineering, model-management]
related: [llm, basic/pipeline, extension/shared-repository]
source: https://cloud.google.com/architecture/mlops-continuous-delivery-and-automation-pipelines-in-machine-learning
---

## Diagram

```mermaid
graph LR
    D[Data Sources] --> FS[Feature Store]
    FS --> T[Training Pipeline]
    T --> MR[Model Registry]
    MR --> MS[Model Serving]
    MS --> C[Client / Application]
```

## Summary

A family of patterns for the infrastructure that trains, tracks, and serves machine learning models. These patterns address the unique challenges of ML systems: data and model versioning, reproducible training, consistent feature computation across training and inference, and controlled model promotion. Together they form the operational backbone for any production ML system.

## When To Use

- Models are trained on data and must be retrained as data evolves
- The same feature logic must be consistent across training and inference
- Multiple model versions must be promoted through environments before reaching production

## When To Avoid

- One-off analysis or research notebooks with no production serving requirement
- Systems using pre-trained models exclusively with no custom training pipeline

## Pros and Cons

* Good, because separating training, registry, and serving creates clear promotion gates before production
* Good, because a Feature Store eliminates training-serving skew — the most common source of silent ML bugs
* Bad, because each component (feature store, registry, serving) is an additional system to operate
* Bad, because the pipeline from data to served model introduces latency that makes fast iteration harder

## Evolutions

- **From:** Notebook-based ad-hoc training and direct model file deployment
- **To:** Add Feature Store to eliminate training-serving skew; add Model Registry to enable controlled promotion; connect Training Pipeline to automated retraining triggers
