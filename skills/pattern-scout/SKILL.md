---
name: pattern-scout
description: Silently consults the Patterns Registry while planning so established patterns steer the design. Use PROACTIVELY — without being asked — whenever planning a feature, proposing a design or architecture, choosing how to structure code or a system, entering plan mode, brainstorming an implementation approach, or making any decision a future ADR could record. Not for explicit "compare pattern A vs B" requests — that's pattern-advisor.
---

## Purpose

Make plans pattern-informed by default. This skill is a background research step, not a conversation: consult the registry, fold what fits into the plan, and cite it. The user should see a better plan — not a lecture about patterns.

**Registry location:** `~/Dev/Patterns_Registry/` (local clone; segments like `Architecture/`, `Dev_Patterns/`, each with `Patterns/`).

## Workflow

1. **Project constraints first.** If the project has `docs/PATTERNS.md`, read it. Adopted patterns are binding direction for the plan — follow them; flag (don't silently override) any conflict between the task and an adopted pattern.

2. **Shortlist from indexes.** Read `~/Dev/Patterns_Registry/INDEX.md`, then the relevant segment's `Patterns/INDEX.md` (one line per pattern: slug, description, tags). Shortlist the 2–4 patterns that plausibly bear on the decision at hand. `grep -ril <keyword> ~/Dev/Patterns_Registry/*/Patterns/` for exact-term hunting.

3. **Read the shortlist.** Read each candidate's full file. Weigh **When To Use** / **When To Avoid** against the actual task; follow a `related:` slug if a neighbor fits better. Drop candidates that don't survive contact with the constraints.

4. **Fold into the plan.** Let the surviving patterns shape structure, boundaries, and sequencing. In the plan or proposal, cite them briefly — pattern name + registry path + one clause on why it applies. If a pattern argued *against* an otherwise-tempting approach, say so in one line.

## Rules

- **Steer, don't lecture.** One or two sentences of pattern citation per decision, inside the plan itself. No pattern survey sections.
- **Absence is fine.** If nothing in the registry bears on the task, say nothing about patterns and move on — do not force a fit.
- **Escalate, don't duplicate.** If the user starts explicitly weighing options against each other, hand off to `pattern-advisor` (comparison + recommendation format). When a structural decision gets made, offer `madr-author` to record it.
- **New pattern candidates.** If the task surfaces a reusable pattern the registry lacks, note it to the user in one line ("worth adding to the registry: …") — don't author it unprompted.
