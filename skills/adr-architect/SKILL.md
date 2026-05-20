---
name: adr-architect
description: Creates Architecture Decision Records (ADRs) in MADR format, drawing on design patterns stored in the kholcomb/Architecture GitHub repository (with metapatterns.io as a fallback reference). Use this skill whenever someone asks to document an architectural decision, says "create an ADR for…", "how should we architect X", "which pattern fits this problem", "we decided to use Y — document it", or describes a technical trade-off that deserves a formal record. Trigger even when the user hasn't said "ADR" — if they're wrestling with an architectural choice, this skill should be used. Also use this skill for questions like "should we use microservices or a monolith", "how do we structure our backend", or "help me compare architectural options".
---

## Purpose

You help engineers make better architectural decisions and leave a durable record of why those decisions were made. A good ADR isn't just documentation — it's institutional memory that prevents the same debate from recurring six months later.

You handle two entry points:

- **Path A — User already knows the pattern/decision**: They say "create an ADR for using Hexagonal Architecture" or "we've decided to go with Services — document it." Jump straight to gathering context and drafting.
- **Path B — User needs pattern guidance**: They describe a problem ("how do we decompose this monolith?"). Fetch relevant patterns from metapatterns.io, present options with trade-offs, confirm the choice, then draft the ADR.

Both paths produce the same thing: a properly numbered, fully filled MADR file saved to `docs/decisions/`.

---

## Step 1 — Gather decision context

Ask this in a single message — don't make the user go back and forth:

- **Problem**: What specific challenge does this decision address? (be concrete)
- **Constraints**: Performance budgets, team skills, existing tech, cost, compliance requirements
- **Stakeholders**: Who decides? Who should be informed?
- **References**: Ticket URL, RFC, GitHub issue, or relevant discussion?
- **Status**: Is this proposed, accepted, or already implemented?

Extract anything already stated in the conversation. Don't re-ask for things they've already told you.

---

## Step 2 — Find relevant patterns

**Primary source: `kholcomb/Architecture` repository**

Patterns live in the `Patterns/` directory of `https://github.com/kholcomb/Architecture`. Use `gh` CLI to discover and read them:

```bash
# List available patterns
gh api repos/kholcomb/Architecture/contents/Patterns

# Read a specific pattern file
gh api repos/kholcomb/Architecture/contents/Patterns/layers.md \
  --jq '.content' | base64 -d
```

Patterns may be organized in subdirectories (e.g., `Patterns/basic/`, `Patterns/implementation/`). If so, list the subdirectory first:

```bash
gh api repos/kholcomb/Architecture/contents/Patterns/basic
```

**Fallback: metapatterns.io**

If the `Patterns/` directory is empty, the pattern isn't there yet, or the repo doesn't exist yet, fall back to fetching directly from metapatterns.io using `WebFetch`:

```
https://metapatterns.io/{category}-metapatterns/{slug}/
```

See `references/metapatterns-index.md` for the full pattern catalog and URL slugs. Tell the user when you're falling back: "I didn't find this pattern in your Architecture repo yet, so I'm pulling the reference from metapatterns.io."

**What to focus on when reading any pattern source**: Applicability (when to use / when to avoid), Performance (latency/throughput implications), Dependencies (how change propagates), and Evolution paths (where this pattern goes as the system grows). These are the sections that matter for an ADR.

### Path A: Known pattern

Confirm you'll use the stated pattern. Use `gh` to check if it's in the repo; if so, read it for any project-specific context or notes the team has added. Then go to Step 3.

### Path B: Recommending a pattern

Identify 2-4 candidate patterns from `references/metapatterns-index.md` based on the problem description. Read each one from the Architecture repo (or metapatterns.io fallback). Present them as a compact comparison:

```
### Option: [Pattern Name]
- Fits your situation because: [specific reasons tied to their constraints]
- Trade-offs to accept: [the real costs, not generic drawbacks]
- Evolves toward: [where this pattern typically goes as complexity grows]
- Source: [GitHub path or metapatterns.io URL]

### Option: [Pattern Name]
...
```

Ask which they'd like to use before proceeding. If they're torn, surface the single most differentiating factor between the top two options.

---

## Step 3 — Draft the MADR

Read `references/madr-template.md` for exact field names and structure. Fill every section — no placeholder text.

**What makes a good ADR vs. a mediocre one:**

- **Context**: Explains the forces at play — team size, performance requirements, existing system state, deadline pressure. Not just "we need to decide X."
- **Decision Drivers**: The specific constraints that made this choice non-obvious. If the drivers are obvious, you haven't dug deep enough.
- **Considered Options**: Always include at least one option you rejected, with reasons why. An ADR with one option is a declaration, not a decision.
- **Decision Outcome**: Name the chosen option and explain why *this* option wins against *these specific* constraints. Don't write generic endorsements.
- **Consequences**: Include negative consequences. Future engineers need the full picture. Hiding downsides creates surprises when the system hits the edge cases you knew about.

In the "More Information" section, link to the pattern source — either the file in `kholcomb/Architecture/Patterns/` or the metapatterns.io page, whichever was used. If there's a ticket or RFC, link that too.

---

## Step 4 — Number and save the ADR

Find the current highest ADR number:

```bash
ls docs/decisions/ 2>/dev/null | grep -E '^[0-9]{4}-' | sort | tail -1
```

Start at `0001` if none exist. Use zero-padded 4-digit numbers (`0001`, `0002`, ...).

Filename format: `NNNN-short-kebab-title.md`  
Save to: `docs/decisions/` in the current project

Create the directory if needed:
```bash
mkdir -p docs/decisions
```

After saving, tell the user the file path and offer to:
- Adjust any section based on their feedback
- Link this ADR to related decisions (e.g., "Supersedes ADR-0003")
- Add a row to `docs/decisions/README.md` if an index exists
