---
name: madr-author
description: Creates Architecture Decision Records in MADR v3.0 format, drawing on design patterns from the kholcomb/Architecture Patterns library. Use whenever someone says "create an ADR for…", "document this decision", "we decided to use Y — write it up", "draft a MADR", "record this architectural choice", or describes a decision that's been made and deserves a formal record. Also trigger when the user has finished exploring pattern options and is ready to commit — even if they don't say "ADR" or "MADR".
---

## Purpose

Turn a made architectural decision into a durable MADR document that explains *why* it was made — so future engineers don't relitigate the same debate. A good ADR captures the forces, the rejected alternatives, and the known costs. Placeholder text and missing sections undermine the whole point.

---

## Step 1 — Gather decision context

Ask for the following in a single message. Extract anything already stated in the conversation — don't re-ask.

- **Problem:** What specific challenge does this decision address?
- **Chosen option:** Which pattern or approach was selected?
- **Constraints:** Performance budgets, team size, existing tech, cost, compliance requirements
- **Stakeholders:** Who decided? Who was consulted? Who should be informed?
- **Status:** proposed / accepted / already implemented
- **References:** Ticket URL, RFC, GitHub issue, prior discussion?

---

## Step 2 — Look up the chosen pattern

Read the pattern file from the local Patterns Registry to get accurate `Pros and Cons` and `Evolutions` for populating the ADR:

```bash
# Find the file (INDEX.md lists every pattern with its path)
grep -i "microservices" ~/Dev/Patterns_Registry/Architecture/Patterns/INDEX.md

# Then Read the pattern file directly, e.g.
# ~/Dev/Patterns_Registry/Architecture/Patterns/basic/services/microservices.md
```

If the local clone is missing, fall back to `gh api repos/kholcomb/Architecture/contents/...`; if the pattern isn't in the registry at all, `WebFetch` its source (e.g. metapatterns.io). Skip this step if the user has already provided sufficient detail about the trade-offs directly.

---

## Step 3 — Draft the MADR

Read `references/madr-template.md` for exact field names, frontmatter structure, and formatting. Fill every section — no placeholder text.

**What separates a good ADR from a mediocre one:**

- **Context:** Forces at play — team size, performance requirements, existing system state, deadline pressure. Not just "we need to decide X."
- **Decision Drivers:** The specific constraints that made this choice non-obvious. If the drivers seem obvious, dig deeper — they should explain why the runner-up wasn't chosen.
- **Considered Options:** Always include at least one rejected option with reasons. An ADR with one option is a declaration, not a decision.
- **Decision Outcome:** Name the chosen option and explain why *this* option wins against *these specific* constraints. No generic endorsements.
- **Consequences:** Include negatives. Future engineers need the full picture — hiding known costs creates surprises.
- **More Information:** Link to the pattern source (GitHub path or metapatterns.io URL) and any ticket, RFC, or related ADR.

---

## Step 4 — Number and save

Find the current highest ADR number:

```bash
ls docs/decisions/ 2>/dev/null | grep -E '^[0-9]{4}-' | sort | tail -1
```

Start at `0001` if none exist. Use zero-padded 4-digit numbers.

Filename: `NNNN-short-kebab-title.md`  
Save to: `docs/decisions/` in the current project (create the directory if it doesn't exist).

After saving, tell the user the file path and offer to:
- Adjust any section based on their feedback
- Link this ADR to related decisions (e.g., "Supersedes ADR-0003")
- Add a row to `docs/decisions/README.md` if an index exists

---

## Step 5 — Record the adoption in `docs/PATTERNS.md`

If the ADR's status is **accepted** and it adopts a registry pattern, update the project's adopted-patterns digest so future agent sessions follow the decision instead of re-deciding:

1. Create `docs/PATTERNS.md` if missing, starting with `# Adopted Patterns`.
2. Append one line per adopted pattern:

   ```markdown
   - [{slug}](~/Dev/Patterns_Registry/{segment}/Patterns/{path}) — {one sentence: how this pattern applies in THIS codebase, naming real directories/modules} — ADR-{NNNN}
   ```

3. If a new ADR supersedes an old one, update or remove the superseded line.
4. If the project's `CLAUDE.md` doesn't yet reference the digest, offer to add:

   ```markdown
   Structural decisions: follow the adopted patterns in docs/PATTERNS.md.
   ```

For **proposed** ADRs, skip this step and mention it will apply once accepted.
