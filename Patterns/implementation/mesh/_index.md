---
name: Mesh
category: implementation
also-known-as: [Peer-to-Peer Network, Distributed Grid]
tags: [peer-to-peer, decentralized, distributed, resilience, scalability]
related: [space-based-architecture, microkernel, hexagonal-architecture]
source: https://github.com/denyspoltorak/metapatterns/wiki/Mesh
---

## Summary
The Mesh pattern organizes all nodes in a system as peers that can communicate directly with any other node without routing through a central coordinator. There is no single point of control — each node holds partial state and participates equally in the network's operation. Mesh topologies are used in service meshes (Istio, Linkerd), peer-to-peer file-sharing networks, blockchain networks, and distributed computing grids. The pattern trades central control for resilience, horizontal scalability, and elimination of coordinator bottlenecks.

## When To Use
- Eliminating a single point of failure or bottleneck is a primary requirement
- The system must scale horizontally by adding nodes without architectural changes
- Data or workload should be distributed across nodes to avoid centralized state
- Nodes must continue operating (potentially in degraded mode) when peers become unavailable

## When To Avoid
- Strong consistency is required — coordinating consensus across all peers is expensive and complex
- Operational simplicity is a priority — mesh topologies are harder to monitor, debug, and reason about
- The problem domain is inherently sequential or requires a global ordering that a coordinator would provide
- The node count is small and fixed — the overhead of mesh coordination outweighs the benefits

## Pros and Cons

* Good, because eliminates central coordinator as a single point of failure or performance bottleneck
* Good, because the system scales horizontally by adding peer nodes without architectural changes
* Good, because individual node failures do not bring down the entire network
* Bad, because achieving consistency across peers requires complex distributed consensus protocols
* Bad, because network partition handling (split-brain scenarios) must be designed for explicitly
* Bad, because observability, debugging, and tracing are significantly harder than in centralized architectures

## Evolutions
- **From:** Client-server or hub-and-spoke architecture (remove the central coordinator to gain resilience)
- **To:** Space-Based Architecture (apply mesh principles to in-memory data distribution for extreme scalability)
