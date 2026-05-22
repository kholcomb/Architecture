# MADR Template (v3.0)

Use this template for every ADR. Fill all fields — remove placeholder text completely.

---

```markdown
---
status: {proposed | rejected | accepted | deprecated | superseded by [ADR-XXXX](XXXX-title.md)}
date: {YYYY-MM-DD when last updated}
deciders: {comma-separated list of people who made the decision}
consulted: {people whose opinions were sought — two-way communication}
informed: {people who were kept up to date — one-way communication}
---
# {Short imperative title: "Use X for Y" or "Adopt X to solve Y"}

## Context and Problem Statement

{2-4 sentences describing the situation and forces at play. Explain WHY this decision needed to be made now. What would happen without it? Link to GitHub issue, Jira ticket, or RFC if one exists.}

## Decision Drivers

* {Most important constraint or force — e.g., "team has no ops expertise"}
* {Second driver — e.g., "system must handle 10K req/sec at p99 < 100ms"}
* {Third driver if applicable}

## Considered Options

* {Option 1 — the chosen one}
* {Option 2 — the runner-up}
* {Option 3 — optional, if genuinely considered}

## Decision Outcome

Chosen option: **"{Option 1}"**, because {explain why this option wins against the specific Decision Drivers above — not generic praise, but concrete reasoning tied to the constraints}.

### Consequences

* Good, because {positive consequence — tied to a Decision Driver above}
* Good, because {another benefit}
* Bad, because {real cost you accept — be honest}
* Bad, because {another known downside}

## Pros and Cons of the Options

### {Option 1}

{One sentence description or link to pattern reference}

* Good, because {argument tied to this system's context}
* Good, because {another benefit}
* Neutral, because {trade-off that's context-dependent}
* Bad, because {real cost}

### {Option 2}

{One sentence description or link}

* Good, because {argument}
* Bad, because {why it lost to Option 1 in this context}

### {Option 3 — if applicable}

* Good, because {argument}
* Bad, because {why it was ruled out}

## More Information

{Links to pattern references, RFCs, design docs, related ADRs, or post-decision validation results.}

{If this decision will be revisited, note the trigger: "Revisit if throughput exceeds 50K req/sec" or "Re-evaluate after Q3 load testing."}
```

---

## Field guidance

**status**: Start as `proposed`. Change to `accepted` once decided. Use `superseded by [ADR-XXXX]` when a later decision replaces this one — don't delete old ADRs, they're history.

**deciders vs. consulted vs. informed**: Deciders made the call. Consulted were asked for input. Informed were notified. Being clear about this prevents "but nobody asked me" conflicts later.

**Title format**: Prefer "Use X for Y" or "Adopt X pattern for Z subsystem" — makes the decision scannable from a file listing without opening the document.

**Consequences vs. Pros/Cons**: Consequences are the *expected outcomes* of the chosen option. Pros/Cons covers *all* options for comparison. Both sections are valuable — don't collapse them.
