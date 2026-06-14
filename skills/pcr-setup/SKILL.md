---
name: pcr-setup
description: Set up Project Context Records (PCR) in the current project — put the PCR adoption block into the project's AGENTS.md (with a CLAUDE.md symlink) and create the records folder, idempotently. Use when the user runs /pcr-setup, or asks to set up, adopt, install, or add PCR / Project Context Records to a project. Do NOT use for writing or editing individual records, or for changing the methodology doc itself.
---

# pcr-setup

Adopt **Project Context Records (PCR)** in the current project: put the PCR
adoption block into the project's agent-instructions file and create the records
folder. Methodology: https://github.com/hyf0/project-context-records

Do this directly with your file tools — it is a few small, reliable edits, no
script needed.

## Steps

- [ ] 1. Find the project root (the git root, else the current directory).
- [ ] 2. Ensure the records folder exists — `.agents/docs/` by default (create it
  if missing). If the user named a different folder, use that.
- [ ] 3. Choose the agent-instructions file:
  - `AGENTS.md` exists → use it.
  - else a *real* `CLAUDE.md` exists (not a symlink) → use it (respect the
    project's existing setup).
  - else → create `AGENTS.md` and symlink `CLAUDE.md` → `AGENTS.md`.
- [ ] 4. **Idempotency:** if the chosen file already contains the line
  `## Project Context Records (PCR)`, stop — PCR is already set up. Tell the user
  and change nothing.
- [ ] 5. Otherwise append the block below **verbatim** (one blank line before it if
  the file is non-empty). If a non-default records folder was used, replace
  `.agents/docs/` in the block with it.
- [ ] 6. Tell the user in one or two lines what changed, and that they can now keep
  records under the folder and vouch a line or a whole file with
  `[VOUCHED @<their-handle>]` — a stamp counts only when a human adds it explicitly.

## The block to inject

```
## Project Context Records (PCR)

This project follows **Project Context Records (PCR)** —
methodology: https://github.com/hyf0/project-context-records. PCR keeps the
project's durable design context — the *why*, the decisions, the architecture —
so you inherit it instead of re-deriving or re-litigating what's already settled.

When working here:
- **Where they live.** Records are in `.agents/docs/` — one topic per file,
  cross-linked with relative Markdown links (`[name](./name.md)`).
- **Read first.** If a record covers the area you're touching, read it before acting.
- **Record as you go.** Proactively write down context worth keeping — and whenever
  a human asks you to. No required format, no fixed list of what qualifies: if it's
  true about this project, not visible in the code, and useful beyond the moment,
  it's worth a record.
- **Keep it fresh.** If your change affects a record, update it in the same change —
  a stale record is a trap, not an asset.
- **Provenance.** An unstamped line is AI-accumulated: challenge and verify it freely.
  A `[VOUCHED @handle]` stamp (on a line, or at the top of a file) means a human
  vouched for it — treat it as settled; reopen or re-verify only on new evidence, a
  changed constraint, or a human's say-so. Add a stamp only on a human's explicit
  instruction; reading past a line, or not objecting, is not a stamp.
```
