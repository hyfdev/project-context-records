---
name: pcr-setup
description: Set up Project Context Records (PCR) in the current project — safely install or update the marked PCR block in the project's AGENTS.md, create the records folder, and offer to seed the starter records, idempotently. Use when the user runs /pcr-setup, or asks to set up, adopt, install, add, update, or re-sync PCR / Project Context Records in a project. Do NOT use for writing or editing individual records, or for changing the methodology doc itself.
---

# pcr-setup

Adopt **Project Context Records (PCR)** in the current project — or, if it is already adopted, update it to the canonical version bundled with this installed skill. The skill itself is a snapshot; the user updates it separately with `npx skills update pcr-setup -g`. Methodology: https://github.com/hyf0/project-context-records

Do this directly with your file tools — it is a few small, reliable edits, no script needed.

## Steps

- [ ] 1. Find the project root (the git root, else the current directory).
- [ ] 2. Ensure the records folder exists — `.agents/docs/` by default (create it if missing). If the user named a different folder, use that.
- [ ] 3. Choose the agent-instructions file:
  - Both `AGENTS.md` and `CLAUDE.md` exist as separate files → use `AGENTS.md`, and suggest making `CLAUDE.md` a symlink to it so every tool reads one file (suggest only — touch nothing beyond the block).
  - `AGENTS.md` exists → use it.
  - else `CLAUDE.md` exists → use it (respect the project's existing setup).
  - else → create `AGENTS.md`.
- [ ] 4. Prepare the project's block: take the canonical marked block below and, if the project's records folder differs from `.agents/docs/`, substitute that path in — named by the user, or read from the "Where they live" bullet of an existing PCR block. The path is the project's choice and survives updates. Before choosing a case below, count exact standalone marker lines. A valid marked block has exactly one `<!-- PCR:START -->` followed by exactly one `<!-- PCR:END -->`. If either marker appears but the pair is missing, duplicated, or reversed, stop and report the ambiguity without editing the file. Otherwise update the agent-instructions file without losing project rules:
  - **Marked block present** → compare everything from `<!-- PCR:START -->` through `<!-- PCR:END -->`. If identical, do nothing. If different, replace that marked region with the prepared block. The methodology owns only the marked region.
  - **Legacy unmarked block present** → find the `## Project Context Records (PCR)` heading and its PCR bullet list, then classify the old text before changing anything. Separate clearly project-specific additions such as local paths, commands, routing, or policies from clearly recognizable earlier canonical wording; an extra named bullet is local by default. If any clause is mixed or could plausibly be either prior methodology text or a local edit, stop without editing and show the user the proposed split for confirmation. Once the split is unambiguous or confirmed, move the project-specific text outside the new PCR markers and every other generated or third-party marker region. Put it under the nearest clearly project-owned instructions heading; if none exists, create `## Project-specific agent instructions` immediately after the PCR block. Preserve its exact wording, then replace only the prior methodology text with the prepared marked block; never silently discard uncertain text.
  - **No block present** → append the prepared block, with one blank line before it if the file is non-empty.
- [ ] 5. If the records folder has no records yet, offer to seed. On a greenfield repo (little or no code yet — typical before an unattended build), there is nothing to describe — seed **direction** instead, drafted from the user's brief: `goal.md` (what it's trying to be, for whom, and the non-goals), the architecture bets as `architecture.md` (it matures from bet to description as code appears), and hard every-session constraints into the agent-instructions file outside the block. The user vouches what must hold before the first run. On an existing codebase, the seed is the **starter set**, drafted from what the repo itself shows (README, manifests, config, git history). First check for existing docs that already cover a topic — `DESIGN.md`, `ARCHITECTURE.md`, `docs/`, an `adr/` folder: **enroll** those instead of duplicating them, with a map route pointing at each where it lives (create the map if needed — records outside the folder are exactly what a map is for). Put machine-checkable constraints in types, tests, lints, or CI and keep only their rationale and reconsideration conditions in prose. Back factual claims with durable evidence, never a temporary path or unpreserved screenshot. Then draft only the gaps — only what the repo gives evidence for, skipping the rest — and leave everything unstamped: it is AI-accumulated until a human reviews and vouches it. The value in each is what stronger artifacts and the code alone *cannot* say — not a restatement of them:
  - `goal.md` — what this is trying to be, for whom, and what it deliberately is not (the non-goals). If the README already states it all, enroll that instead.
  - `technology-stack.md` — why these tools over the defaults they displaced, what must not be introduced, what is pinned and why. Not a manifest dump.
  - `architecture.md` — the units, the boundaries between them, and why the lines are where they are.
  - `conventions.md` — where this project deliberately departs from ecosystem defaults, so departures read as decisions.
  - `gotchas.md` — traps already paid for: things that look safe and aren't, each with its why.
  - `DESIGN.md` — only if the project has a visual surface (a UI, a site, themed output): its visual identity for coding agents — design tokens plus their why — following the design.md spec (https://github.com/google-labs-code/design.md). Draft it at the repo root (that convention's home) and enroll it in the map. Whenever a `DESIGN.md` exists — found or drafted — suggest its linter (`npx @google/design.md lint DESIGN.md`); for a project with no visual surface, don't mention the file or the linter at all.
- [ ] 6. Tell the user in one or two lines what changed, including any legacy project rules moved outside the markers. Say that records live under the folder and a human can explicitly vouch a line, section, or whole file with `[VOUCHED @<their-handle> YYYY-MM-DD]`. If records were seeded, say they are unstamped drafts awaiting review.

## The block to inject

```
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
```
