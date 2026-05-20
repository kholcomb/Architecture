# Architecture Pattern Knowledge Base

Normalized descriptions of software architecture patterns, sourced from [metapatterns.io](https://metapatterns.io/). Consumed by the `adr-architect` skill to generate contextually grounded MADRs.

## Table of Contents

- [Architecture Pattern Knowledge Base](#architecture-pattern-knowledge-base)
  - [Table of Contents](#table-of-contents)
  - [Overview](#overview)
  - [Pattern Categories](#pattern-categories)
    - [Basic](#basic)
    - [Extension](#extension)
    - [Fragmented](#fragmented)
    - [Implementation](#implementation)
  - [Schema](#schema)
  - [Skills](#skills)

## Overview

Each file represents one architectural option. The `adr-architect` skill combines multiple pattern files into a single [MADR](https://adr.github.io/madr/)-formatted Architecture Decision Record.

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

## Schema

Patterns follow a structured frontmatter + body format. Fields include `name`, `category`, `tags`, `related`, and `source`. Body sections map directly to MADR fields.

Full spec: [`Patterns/_schema.md`](Patterns/_schema.md)

## Skills

| Skill | Location | Purpose |
|-------|----------|---------|
| `adr-architect` | [`skills/adr-architect/`](skills/adr-architect/) | Generates MADRs from pattern files |
