# Architecture Pattern Knowledge Base — Schema

## Purpose

Normalized descriptions of software architecture patterns from [metapatterns.io](https://metapatterns.io/). Consumed by the ADR-generating skill to produce contextually grounded MADRs.

Each file represents one architectural option. The skill combines multiple pattern files into a single MADR.

## File Organization

```
ADR/patterns/
├── {category}/
│   ├── _index.md        # the metapattern
│   └── {sub-pattern}.md # concrete patterns within this metapattern
```

Metapatterns with no selected sub-patterns remain as flat `.md` files (no folder).

Categories: `basic`, `extension`, `fragmented`, `implementation`, `operational`, `security`, `ai`

## Schema

### Frontmatter

```yaml
---
name: {Display Name}
category: {category/subcategory}    # e.g. extension/proxy
also-known-as: []                   # empty list if no aliases
tags: []                            # searchable keywords
parent: {filename-slug}             # filename without .md, e.g. "proxy"
                                    # omit this field entirely for metapatterns
related: []                         # filename slugs of related patterns
source: {url}                       # canonical source page
---
```

### Body Sections

```markdown
## Summary
One paragraph. What this pattern is and the architectural problem it addresses.

## When To Use
- Condition or signal that makes this pattern appropriate

## When To Avoid
- Condition or signal that makes this pattern a poor fit

## Pros and Cons

* Good, because {argument}
* Bad, because {argument}

## Evolutions
- **From:** {patterns that typically precede this one}
- **To:** {patterns this naturally grows into}
```

## MADR Mapping

Each pattern file represents one option in an ADR:

| Pattern section | MADR section |
|---|---|
| `Summary` | Entry in **Considered Options** + context for **Context and Problem Statement** |
| `When To Use` / `When To Avoid` | **Decision Drivers** |
| `Pros and Cons` | **Pros and Cons of the Options** for this option |
| `Evolutions` | **Consequences** + **More Information** |
| `related` | **More Information** links |

For deeper detail on any pattern, fetch the `source` URL.

## Authoring Guide

- One pattern per file — no exceptions
- Bullet-first style — minimal prose
- `Pros and Cons` uses `* Good, because` / `* Bad, because` verbatim (matches MADR format)
- Keep files lean — `source` is the deep reference
- `related` values are filename slugs, not display names (e.g. `proxy` not `"Proxy"`)
- `actors.md` exists in both `shards/` and `services/` intentionally — different contexts, independent files
