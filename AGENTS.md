# AGENTS.md

**This file is the single source of truth for working in this repo.** `CLAUDE.md` is a symlink to it — never edit `CLAUDE.md` directly; edit `AGENTS.md`, and the change reaches every tool at once.

## What this repo is

This repo *is* the **Project Context Records (PCR)** methodology. The canonical document is `README.md`. The repo dogfoods itself: the records under `.agents/docs/` cover PCR's own design decisions, and `README.md` — the methodology — is the "code" they describe.

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

## Canonical copies stay in sync

Two families of by-design copies exist; a change to one member updates the others in the same commit:

- **The adoption block** lives in `README.md` ("How to use"), in `skills/pcr-setup/SKILL.md`, and installed above in this file — all three byte-identical. Editing the block means editing all three; re-running `/pcr-setup` in this repo refreshes this file's copy, so every block change is also a live test of the update path.
- **The translation.** `README.md` (English) is the source of truth; `README.zh-CN.md` must track it exactly — a drifted translation is worse than none: it silently misinforms. When the two disagree, `README.md` wins; fix the translation to match. Keep the coined terms (Project Context Records / PCR, Context Engineering, ADR, the provenance stamp), every URL, and the adoption block identical and untranslated across both files.

## Repo conventions

- **Soft-wrap only.** Write each paragraph or bullet as a single physical line and let the editor wrap; never insert a manual line break mid-sentence.
