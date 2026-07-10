# AGENTS.md

**This file is the single source of truth for working in this repo.** `CLAUDE.md` is a symlink to it — never edit `CLAUDE.md` directly; edit `AGENTS.md`, and the change reaches every tool at once.

## What this repo is

This repo *is* the **Project Context Records (PCR)** methodology. The canonical document is `README.md`. The repo dogfoods itself: the records under `.agents/docs/` cover PCR's own design decisions, and `README.md` — the methodology — is the "code" they describe.

<!-- PCR:START -->
## Project Context Records (PCR)

This project follows **Project Context Records (PCR)** — methodology: https://github.com/hyf0/project-context-records. PCR keeps the project's durable design context — the *why*, the decisions, the architecture — so you inherit it instead of re-deriving or re-litigating what's already settled.

When working here:
- **Where they live.** Records are in `.agents/docs/`, one topic per file, cross-linked with relative Markdown links. A `README.md` there is the **map**: it routes code areas or hotspots to the exact record or heading. Create one when retrieval stops being a glance or one record grows into a long ledger.
- **Read first.** Start from the map if present, else scan the folder. Open the exact records or headings that cover an area before changing or answering for it.
- **Use the strongest durable form.** Put machine-checkable constraints in types, tests, lints, or CI; put local rationale beside the code with a link; use PCR for cross-cutting judgment, intent, and other context that must remain prose.
- **Record as you go.** Capture context when a decision lands, a trap costs you, a human corrects you, or a human asks. If it is true about this project, not durable in a stronger form, and useful beyond the moment, it is worth a record. Report records you change so a human can review or vouch them.
- **Keep it fresh.** Update affected records with the same change. When code and a record disagree, decide whether implementation drifted from intent or description went stale, then update the stale side; surface a vouched conflict. Back facts with durable evidence such as tests, reproducible commands, committed artifacts, stable URLs, or commit hashes — not ephemeral paths or missing screenshots.
- **Provenance.** Unstamped text is AI-accumulated: challenge and verify it freely. `[VOUCHED @handle YYYY-MM-DD]` means the named human explicitly accepts the covered words as current project direction, not that a factual claim is proven. At a non-heading line's end it covers that line; as the first nonblank line below a non-title heading it covers that section; as the first nonblank line below the document title it covers the file. Never put a new stamp in heading text: it breaks link anchors. Legacy stamps before a title or in a heading retain the project's prior scope; never move or reinterpret them without explicit human approval. Add one only on explicit instruction. A stamp added by work under review counts only if the named human confirms it; an unchanged stamp on the target branch is inherited project state. Material edits or scope-boundary changes remove stamps; formatting keeps them only if the covered words stay identical. Legacy undated stamps remain valid until re-vouched.
- **Distill when a human reviews.** Accumulation is noisy by design; the valve is a human review pass. Draft what to prune, merge, or promote, and flag vouches plausibly affected by changes to the areas or evidence they cover. The human decides and vouches.
- **Unattended.** With no human between iterations: keep the running plan as one live record, overwritten as truth changes; tidy your own unstamped layer — merge duplicates, prune dead notes — never the vouched one; when evidence argues with vouched direction, record the conflict and stay inside that direction unless progress becomes impossible; end by drafting the distillation for the returning human, conflicts included. No run, however long or green, vouches anything.
- **The basics.** The recommended starting list — most projects need these; draft the missing ones that apply:
  - `goal.md` — audience, goal, and non-goals; enroll the README instead if it already covers them.
  - `technology-stack.md` — why tools, restrictions, or pins exist; not a manifest dump.
  - `architecture.md` — units, boundaries, and why the lines are where they are.
  - `conventions.md` — deliberate departures from ecosystem defaults.
  - `gotchas.md` — traps already paid for, each with its why.
  - `DESIGN.md` — only for a visual surface; follow https://github.com/google-labs-code/design.md, keep it at the root, and enroll it in the map.
<!-- PCR:END -->

## Canonical copies stay in sync

Two families of by-design copies exist; a change to one member updates the others in the same commit:

- **The adoption block** includes its `PCR:START` / `PCR:END` markers and lives in `README.md`, `README.zh-CN.md`, `skills/pcr-setup/SKILL.md`, and above in this file — all four byte-identical. Editing the block means editing all four; after updating the installed skill, re-running `/pcr-setup` in this repo refreshes this file's copy, so every block change is also a live test of the update path.
- **The translation.** `README.md` (English) is the source of truth; `README.zh-CN.md` must track it exactly — a drifted translation is worse than none: it silently misinforms. When the two disagree, `README.md` wins; fix the translation to match. Keep the coined terms (Project Context Records / PCR, Context Engineering, ADR, the provenance stamp), every URL, and the adoption block identical and untranslated across both files.

## Repo conventions

- **Soft-wrap only.** Write each paragraph or bullet as a single physical line and let the editor wrap; never insert a manual line break mid-sentence.
