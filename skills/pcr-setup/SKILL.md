---
name: pcr-setup
description: Set up Project Context Records (PCR) in the current project — put the PCR adoption block into the project's AGENTS.md, create the records folder, and offer to seed the starter records, idempotently. Use when the user runs /pcr-setup, or asks to set up, adopt, install, add, update, or re-sync PCR / Project Context Records in a project. Do NOT use for writing or editing individual records, or for changing the methodology doc itself.
---

# pcr-setup

Adopt **Project Context Records (PCR)** in the current project — or, if it is already adopted, update it: re-running syncs the block to the canonical version below and touches nothing else. Methodology: https://github.com/hyf0/project-context-records

Do this directly with your file tools — it is a few small, reliable edits, no script needed.

## Steps

- [ ] 1. Find the project root (the git root, else the current directory).
- [ ] 2. Ensure the records folder exists — `.agents/docs/` by default (create it
  if missing). If the user named a different folder, use that.
- [ ] 3. Choose the agent-instructions file:
  - Both `AGENTS.md` and `CLAUDE.md` exist as separate files → use `AGENTS.md`, and suggest making `CLAUDE.md` a symlink to it so every tool reads one file (suggest only — touch nothing beyond the block).
  - `AGENTS.md` exists → use it.
  - else `CLAUDE.md` exists → use it (respect the project's existing setup).
  - else → create `AGENTS.md`.
- [ ] 4. Prepare the project's block: take the canonical block below and, if the project's records folder differs from `.agents/docs/`, substitute that path in — named by the user, or read from the "Where they live" bullet of an existing PCR block (the path is the project's choice and survives updates). Then look for an existing PCR block — a `## Project Context Records (PCR)` heading through the end of its bullet list — and compare:
  - **Not present** → append the prepared block (one blank line before it if the file is non-empty).
  - **Present and identical** → nothing to do; tell the user PCR is already up to date.
  - **Present but different** → replace the whole block in place with the prepared one. Local edits inside the block are overwritten by design — the block is the methodology's; everything outside it, records included, stays untouched.
- [ ] 5. If the records folder has no records yet, offer to seed. On a greenfield repo (little or no code yet — typical before an unattended build), there is nothing to describe — seed **direction** instead, drafted from the user's brief: `goal.md` (what it's trying to be, for whom, and the non-goals), the architecture bets as `architecture.md` (it matures from bet to description as code appears), and hard every-session constraints into the agent-instructions file outside the block. The user vouches what must hold before the first run. On an existing codebase, the seed is the **starter set**, drafted from what the repo itself shows (README, manifests, config, git history). First check for existing docs that already cover a topic — `DESIGN.md`, `ARCHITECTURE.md`, `docs/`, an `adr/` folder: **enroll** those instead of duplicating them, with a map row pointing at each where it lives (create the map if needed — records outside the folder are exactly what a map is for). Then draft only the gaps. The value in each is what the code *can't* say — not a restatement of it:
  - `goal.md` — what this is trying to be, for whom, and what it deliberately is not (the non-goals). If the README already states it all, enroll that instead.
  - `technology-stack.md` — why these tools over the defaults they displaced, what must not be introduced, what is pinned and why. Not a manifest dump.
  - `architecture.md` — the units, the boundaries between them, and why the lines are where they are.
  - `conventions.md` — where this project deliberately departs from ecosystem defaults, so departures read as decisions.
  - `gotchas.md` — traps already paid for: things that look safe and aren't, each with its why.
  - `DESIGN.md` — only if the project has a visual surface (a UI, a site, themed output): its visual identity for coding agents — design tokens plus their why — following the design.md spec (https://github.com/google-labs-code/design.md). Draft it at the repo root (that convention's home) and enroll it in the map. Whenever a `DESIGN.md` exists — found or drafted — suggest its linter (`npx @google/design.md lint DESIGN.md`); for a project with no visual surface, don't mention the file or the linter at all.
  Draft only what the repo gives evidence for and skip the rest; leave everything unstamped — it is AI-accumulated until a human reviews and vouches it.
- [ ] 6. Tell the user in one or two lines what changed, and that they can now keep records under the folder and vouch a line or a whole file with `[VOUCHED @<their-handle>]` — a stamp counts only when a human adds it explicitly. If records were seeded, say they are unstamped drafts awaiting review.

## The block to inject

```
## Project Context Records (PCR)

This project follows **Project Context Records (PCR)** — methodology: https://github.com/hyf0/project-context-records. PCR keeps the project's durable design context — the *why*, the decisions, the architecture — so you inherit it instead of re-deriving or re-litigating what's already settled.

When working here:
- **Where they live.** Records are in `.agents/docs/`, one topic per file, cross-linked with relative Markdown links (`[name](./name.md)`). A `README.md` there is the **map** — each record listed with the code it covers, kept in sync with the folder; once the folder outgrows a glance, distill one.
- **Read first.** Start from the map if there is one, else scan the folder. Open what covers an area before you change it — or answer for it.
- **Record as you go.** Write down context worth keeping the moment it appears — a decision lands, a trap costs you, a human corrects you — and whenever a human asks. No required format, no fixed list of what qualifies: if it's true about this project, not visible in the code, and useful beyond the moment, it's worth a record. Mention the records you add or change — what a human never sees never gets vouched.
- **Keep it fresh.** If your change affects a record, update it in the same change — a stale record is a trap, not an asset. When the code contradicts a record, fix the record; if it's vouched, surface the conflict instead of silently overriding.
- **Provenance.** An unstamped line is AI-accumulated: challenge and verify it freely. A `[VOUCHED @handle]` stamp (on a line, or at the top of a file) means a human vouched for it — treat it as settled; reopen or re-verify only on new evidence, a changed constraint, or a human's say-so. Add a stamp only on a human's explicit instruction, and date it when you do (`[VOUCHED @handle 2026-07-08]`); reading past a line, or not objecting, is not a stamp. A stamp covers the words it sits on: materially edit a vouched line and the stamp comes off until a human re-vouches; formatting-only changes keep it.
- **Distill when a human reviews.** Accumulation is noisy by design; the valve is a human review pass. Draft it for them: propose what to prune, merge, or promote, and flag vouches older than the code they cover — the human approves and vouches. Finding is yours; deciding is theirs.
- **Unattended.** With no human between iterations: keep the running plan as one live record, overwritten as truth changes; tidy your own unstamped layer — merge duplicates, prune dead notes — never the vouched one; when evidence argues with a vouched call, record the conflict and stay inside the call unless progress becomes impossible; end the run by drafting the distillation for the human who returns, conflicts included. No run, however long or green, vouches anything.
- **The basics.** The one fixed list — nearly every project needs these; draft the missing ones that apply:
  - `goal.md` — what this project is trying to be, for whom, and what it deliberately is not (the non-goals). The most upstream record; if the README already states it all, give it a map row instead of writing a twin.
  - `technology-stack.md` — why these tools over the defaults, what must not be introduced, what is pinned and why; not a manifest dump.
  - `architecture.md` — the units, the boundaries between them, and why the lines are where they are.
  - `conventions.md` — deliberate departures from ecosystem defaults, so they read as decisions.
  - `gotchas.md` — traps already paid for, each with its why.
  - `DESIGN.md` — only for a project with a visual surface: its visual identity for coding agents — design tokens plus their why — per the design.md spec (google-labs-code/design.md); lives at the root, enrolled in the map.
```
