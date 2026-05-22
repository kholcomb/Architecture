# Metapatterns Quick Reference

Source: https://metapatterns.io  
URL pattern: `https://metapatterns.io/{category}-metapatterns/{slug}/`

---

## Problem → Pattern mapping

Use this to quickly identify which patterns to fetch and evaluate for a given problem.

### "We're starting a new system / greenfield"
- **Layers** — default for small-to-medium projects with specialized teams
- **Monolith** — when simplicity and fast iteration matter most at small scale
- **Hexagonal Architecture** — when infrastructure swappability is a day-one requirement

### "We need to split a monolith"
- **Services** — independent deployment, team autonomy; requires distributed systems discipline
- **Sandwich** — services layer wrapping a shared domain; lower coordination cost than pure services
- **Shards** — partition by data/tenant rather than capability; simpler operationally

### "We need to coordinate between multiple services"
- **Orchestrator** — central coordinator; simpler debugging, single point of failure
- **Middleware** — async message bus; decoupled but harder to trace
- **Layered Services** — hierarchy of services calling services; natural for domain-driven decomposition

### "We need to abstract or extend an existing system"
- **Proxy** — intercept/translate without modifying the target
- **Plugins** — extend behavior without changing core; requires stable plugin API
- **Microkernel** — minimal core with pluggable extensions; good for product platforms

### "We have multiple frontend clients (mobile, web, partner API)"
- **Backends for Frontends (BFF)** — one backend per client type; avoids one-size-fits-all API
- **Proxy** — single gateway with client-specific routing; simpler to maintain

### "We have different data storage needs per subdomain"
- **Polyglot Persistence** — each service owns its own database technology
- **Shared Repository** — shared data store with explicit schema contracts; less operational overhead

### "We need to process data sequentially / transform streams"
- **Pipeline** — linear stages; excellent for ETL, media processing, ML inference
- **Middleware** — async, fan-out; better when stages run at different rates

### "We need a mesh / peer-to-peer topology"
- **Mesh** — all nodes communicate directly; no central coordinator; good for edge/IoT

### "Multiple related systems organized under a parent"
- **Hierarchy** — tree of orchestrating services; good for enterprise integration
- **Service-Oriented Architecture (SOA)** — shared services with enterprise service bus; higher governance cost

---

## All patterns by category

### Basic Metapatterns
| Pattern | Slug | Best for |
|---------|------|---------|
| Monolith | `monolith` | Small teams, fast iteration, low operational complexity |
| Layers | `layers` | Medium projects, team specialization by concern |
| Pipeline | `pipeline` | Sequential data transformation, ETL, ML inference |
| Services | `services` | Independent deployment, team autonomy at scale |
| Shards | `shards` | Horizontal scaling by data partition or tenant |

### Extension Metapatterns
| Pattern | Slug | Best for |
|---------|------|---------|
| Middleware | `middleware` | Async integration, event-driven fan-out |
| Orchestrator | `orchestrator` | Centralized workflow coordination |
| Proxy | `proxy` | Abstraction, translation, routing without modifying targets |
| Shared Repository | `shared-repository` | Cross-service data sharing with lower coordination cost |
| Sandwich | `sandwich` | Services layer over shared domain |

### Fragmented Metapatterns
| Pattern | Slug | Best for |
|---------|------|---------|
| Layered Services | `layered-services` | Hierarchical service dependencies |
| SOA | `service-oriented-architecture--soa-` | Enterprise integration, shared business services |
| Backends for Frontends | `backends-for-frontends--bff-` | Multiple client types needing different APIs |
| Polyglot Persistence | `polyglot-persistence` | Per-service database technology optimization |
| Hierarchy | `hierarchy` | Multi-level orchestration trees |

### Implementation Metapatterns
| Pattern | Slug | Best for |
|---------|------|---------|
| Hexagonal Architecture | `hexagonal-architecture` | Swappable infrastructure, testability, domain purity |
| Microkernel | `microkernel` | Extensible platforms, plugin ecosystems |
| Mesh | `mesh` | Peer-to-peer, edge computing, IoT |
| Plugins | `plugins` | Runtime extensibility without core changes |

---

## Useful comparison pages

- Dependency inversion patterns: `https://metapatterns.io/analytics/comparison-of-architectural-patterns/dependency-inversion-in-architectural-patterns/`
- Sharing data among services: `https://metapatterns.io/analytics/comparison-of-architectural-patterns/sharing-functionality-or-data-among-services/`
- Architecture and product lifecycle: `https://metapatterns.io/analytics/architecture-and-product-life-cycle/`
- Ambiguous patterns (common confusions): `https://metapatterns.io/analytics/ambiguous-patterns/`
