---
name: pattern-advisor
description: Explores and compares architecture patterns from the kholcomb/Architecture Patterns library to help you choose the right pattern for a problem. Use when someone describes an architectural challenge, asks "which pattern fits X", "how should we structure Y", "compare microservices vs monolith", "what pattern should we use", "help me pick an architecture", or is wrestling with a structural trade-off — even if they haven't said "pattern". Trigger proactively when the user is exploring options, not just when they say the word.
---

## Purpose

Help engineers select the right architectural pattern by surfacing what's in the kholcomb/Architecture `Patterns/` library, making trade-offs concrete, and giving a clear recommendation — not a list to decide from.

---

## Step 1 — Understand the problem

Gather context in a single message. Extract anything already stated in the conversation; don't re-ask.

- **What problem are you solving?** (be specific — "hitting throughput bottlenecks at 500 req/sec" beats "scaling issues")
- **Constraints:** team size, performance budgets, existing tech stack, cost, compliance
- **What's not working now?** (current pain or limitations of the existing structure)
- **Stage:** greenfield, refactoring, or expanding an existing system?

---

## Step 2 — Identify candidates

Use `references/metapatterns-index.md` to map the described problem to 2–4 candidate patterns. Then read the relevant pattern files from the Architecture repo:

```bash
# List a subdirectory
gh api repos/kholcomb/Architecture/contents/Patterns/basic/services

# Read a specific pattern file
gh api repos/kholcomb/Architecture/contents/Patterns/basic/services/microservices.md \
  --jq '.content' | base64 -d
```

Patterns may be flat files (`monolith.md`) or indexed metapatterns with sub-patterns under `_index.md`. For each candidate, focus on: **When To Use**, **When To Avoid**, **Pros and Cons**, and **Evolutions**.

If a pattern isn't in the repo yet, fall back to `WebFetch` from metapatterns.io using the URL in the `source` frontmatter field. Tell the user when you do this: "This pattern isn't in your repo yet — pulling from metapatterns.io."

---

## Step 3 — Present a comparison

Present candidates in this format:

```
### Option: [Pattern Name]
- Fits because: [specific reasons tied to their constraints]
- Trade-offs to accept: [real costs, not generic drawbacks]
- Evolves toward: [where this typically goes as complexity grows]
- Source: [GitHub path or metapatterns.io URL]
```

Keep each option tight — this is a comparison aid, not a lecture. If relevant sub-patterns exist (e.g., Microservices or Service-Based Architecture under Services), mention them briefly after the parent.

---

## Step 4 — Recommend

Don't leave the user to decide unaided. State which pattern fits best given *their specific constraints*, and explain why the runner-up loses on this particular problem. If they're genuinely torn, name the single most differentiating factor that should drive the choice — don't make them resolve it themselves.

---

## Step 5 — Offer next step

Once a pattern is chosen, offer: "When you're ready to document this decision, the `madr-author` skill can draft the ADR for you."
