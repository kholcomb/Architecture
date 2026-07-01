# Architecture Pattern Knowledge Base

Normalized descriptions of software architecture patterns, sourced from [metapatterns.io](https://metapatterns.io/) and other authoritative catalogs (Azure Architecture Center, OpenTelemetry, NIST, OWASP, Anthropic, and more). Consumed by the `madr-author` and `pattern-advisor` skills.

## Table of Contents

- [Architecture Pattern Knowledge Base](#architecture-pattern-knowledge-base)
  - [Table of Contents](#table-of-contents)
  - [Overview](#overview)
  - [Pattern Categories](#pattern-categories)
    - [Basic](#basic)
    - [Extension](#extension)
    - [Fragmented](#fragmented)
    - [Implementation](#implementation)
    - [Operational](#operational)
    - [Security](#security)
    - [AI](#ai)
  - [Schema](#schema)
  - [Skills](#skills)

## Overview

Each file represents one architectural option. The `madr-author` skill combines multiple pattern files into a single [MADR](https://adr.github.io/madr/)-formatted Architecture Decision Record, and the `pattern-advisor` skill explores and compares them to help select the right pattern for a problem.

The `basic`, `extension`, `fragmented`, and `implementation` categories are drawn from [metapatterns.io](https://metapatterns.io/). The `operational`, `security`, and `ai` categories extend the taxonomy into adjacent domains, each sourced from that domain's authoritative references (cited per file).

See [`Patterns/_schema.md`](Patterns/_schema.md) for the full authoring spec and MADR field mapping.

## Pattern Categories

### Basic

Foundational deployment and structural shapes.

| Pattern |
| --- |
| [Monolith](Patterns/basic/monolith.md) |
| [Layers](Patterns/basic/layers/) |
| [Pipeline](Patterns/basic/pipeline/) |
| [Services](Patterns/basic/services/) |
| [Shards](Patterns/basic/shards/) |

### Extension

Patterns that extend or wrap existing systems.

| Pattern |
| --- |
| [Middleware](Patterns/extension/middleware/) |
| [Orchestrator](Patterns/extension/orchestrator/) |
| [Proxy](Patterns/extension/proxy/) |
| [Sandwich](Patterns/extension/sandwich.md) |
| [Shared Repository](Patterns/extension/shared-repository.md) |

### Fragmented

Distributed and decomposed system shapes.

| Pattern |
| --- |
| [Backends for Frontends](Patterns/fragmented/backends-for-frontends.md) |
| [Hierarchy](Patterns/fragmented/hierarchy/) |
| [Layered Services](Patterns/fragmented/layered-services/) |
| [Polyglot Persistence](Patterns/fragmented/polyglot-persistence/) |
| [Service-Oriented Architecture](Patterns/fragmented/service-oriented-architecture/) |

### Implementation

Cross-cutting structural and plugin patterns.

| Pattern |
| --- |
| [Hexagonal Architecture](Patterns/implementation/hexagonal-architecture/) |
| [Mesh](Patterns/implementation/mesh/) |
| [Microkernel](Patterns/implementation/microkernel/) |
| [Plugins](Patterns/implementation/plugins.md) |

### Operational

Runtime concerns: deploying, observing, and keeping systems resilient.

| Pattern |
| --- |
| [Deployment](Patterns/operational/deployment/) |
| [Observability](Patterns/operational/observability/) |
| [Resilience](Patterns/operational/resilience/) |

### Security

Structural patterns for trust, authentication, authorization, and safe failure.

| Pattern |
| --- |
| [Zero Trust](Patterns/security/zero-trust.md) |
| [Security Zones](Patterns/security/security-zones.md) |
| [Claims-Based Identity](Patterns/security/claims-based-identity.md) |
| [Federated Identity](Patterns/security/federated-identity.md) |
| [Gateway Authentication](Patterns/security/gateway-authentication.md) |
| [Service Identity](Patterns/security/service-identity.md) |
| [Valet Key](Patterns/security/valet-key.md) |
| [Sandboxing](Patterns/security/sandboxing.md) |
| [Fail Secure](Patterns/security/fail-secure.md) |

### AI

Patterns for systems built on LLMs and machine-learning models.

| Pattern |
| --- |
| [LLM Applications](Patterns/ai/llm/) |
| [ML Systems](Patterns/ai/ml-systems/) |

## Schema

Patterns follow a structured frontmatter + body format. Fields include `name`, `category`, `also-known-as`, `tags`, `parent`, `related`, and `source`. Body sections map directly to MADR fields.

Full spec: [`Patterns/_schema.md`](Patterns/_schema.md)

## Skills

| Skill | Location | Purpose |
|-------|----------|---------|
| `madr-author` | [`skills/madr-author/`](skills/madr-author/) | Generates MADR-format ADRs from pattern files |
| `pattern-advisor` | [`skills/pattern-advisor/`](skills/pattern-advisor/) | Explores and compares patterns to select the right one |
