---
name: pcr-setup
description: Set up Project Context Records (PCR) in the current project — safely install or update the marked PCR block in the project's AGENTS.md, create the records folder, and offer to seed the suggested topic records, idempotently. Also opens an area decision ledger on the user's declaration. Use when the user runs /pcr-setup, asks to set up, adopt, install, add, update, or re-sync PCR / Project Context Records in a project, or declares that an area should record decisions. Do NOT use for writing or editing individual records, or for changing the methodology doc itself.
---

# pcr-setup

Adopt **Project Context Records (PCR)** in the current project — or, if it is already adopted, update it to the canonical version bundled with this installed skill. The skill itself is a snapshot; the user updates it separately with `npx skills update pcr-setup -g`. Methodology: https://github.com/hyfdev/project-context-records

Do this directly with your file tools — it is a few small, reliable edits, no script needed.

## Steps

- [ ] 1. Find the project root (the git root, else the current directory).
- [ ] 2. Ensure the records folder exists — `.agents/docs/` by default (create it if missing). If the user named a different folder, use that.
- [ ] 3. Choose the agent-instructions file:
  - Both `AGENTS.md` and `CLAUDE.md` exist as separate files → use `AGENTS.md`, and suggest making `CLAUDE.md` a symlink to it so every tool reads one file (suggest only — touch nothing beyond the block).
  - `AGENTS.md` exists → use it.
  - else `CLAUDE.md` exists → use it (respect the project's existing setup).
  - else → create `AGENTS.md`.
- [ ] 4. Prepare the project's block: take the canonical marked block below and, if the project's records folder differs from `.agents/docs/`, substitute that path in — named by the user, or read from the "Where records live" bullet of an existing PCR block (older blocks name it "Where they live"). The path is the project's choice and survives updates. Before choosing a case below, count exact standalone marker lines. A valid marked block has exactly one `<!-- PCR:START -->` followed by exactly one `<!-- PCR:END -->`. If either marker appears but the pair is missing, duplicated, or reversed, stop and report the ambiguity without editing the file. Otherwise update the agent-instructions file without losing project rules:
  - **Marked block present** → compare everything from `<!-- PCR:START -->` through `<!-- PCR:END -->`. If any other generated or third-party marker line sits inside that region, stop and report it without editing, as with a malformed pair — replacing across it would corrupt the other tool's marked region. If identical, do nothing. If different, replace that marked region with the prepared block. The methodology owns only the marked region.
  - **Legacy unmarked block present** → find the `## Project Context Records (PCR)` heading and its PCR bullet list, then classify the old text before changing anything. Separate clearly project-specific additions such as local paths, commands, routing, or policies from clearly recognizable earlier canonical wording; an extra named bullet is local by default. If any clause is mixed or could plausibly be either prior methodology text or a local edit, stop without editing and show the user the proposed split for confirmation. Once the split is unambiguous or confirmed, move the project-specific text outside the new PCR markers and every other generated or third-party marker region. Put it under the nearest clearly project-owned instructions heading; if none exists, create `## Project-specific agent instructions` immediately after the PCR block. Preserve its exact wording, then replace only the prior methodology text with the prepared marked block; never silently discard uncertain text.
  - **No block present** → append the prepared block, with one blank line before it if the file is non-empty.
- [ ] 5. If the records folder has no records yet, offer to seed:
  - **Greenfield repo** (little or no code yet — typical before an unattended run): there is nothing to describe, so seed **direction** instead, drafted from the user's description — `intent.md` (what it is trying to be, for whom, and the non-goals) and the architecture bets as `architecture.md` (it matures from bet to description as code appears). Hard every-session constraints go into the agent-instructions file outside the block. The user vouches what must hold before the first run.
  - **Existing codebase**: the seed is the **suggested topics**, drafted from what the repo itself shows (README, manifests, config, git history). First check for existing docs that already cover a topic — `DESIGN.md`, `ARCHITECTURE.md`, `docs/`, an `adr/` folder: **enroll** those instead of duplicating them, with a map route pointing at each where it lives (create the map if needed — records outside the folder are exactly what a map is for). Leave machine-checkable constraints to the repository's own types, tests, lints, or CI — seeding drafts records, never enforcement — and keep only their rationale and reconsideration conditions in prose. Back factual claims with durable evidence, never a temporary path or unpreserved screenshot. Then draft only the gaps — only what the repo gives evidence for, skipping the rest — and leave everything unstamped: it is AI-accumulated until a human reviews and vouches it. The value in each is what stronger artifacts and the code alone *cannot* say — not a restatement of them:
    - `intent.md` — what this is trying to be, for whom, and what it deliberately is not (the non-goals). If the README truly states it all, enroll that instead.
    - `technology-stack.md` — why these tools over the defaults they displaced, what must not be introduced, what is pinned and why. Not a manifest dump.
    - `architecture.md` — the units, the boundaries between them, and why the lines are where they are. Only when the structure isn't glanceable from the code.
    - `gotchas.md` — traps already paid for: things that look safe and aren't, each with its why. Only real paid lessons — never invent "common pitfalls" to fill the file.
    - `DESIGN.md` — only if the project has a visual surface (a UI, a site, themed output): its visual identity for coding agents — design tokens plus their why — following the design.md spec (https://github.com/google-labs-code/design.md). Draft it at the repo root (that convention's home) and enroll it in the map. Whenever a `DESIGN.md` exists — found or drafted — suggest wiring its linter (`npx @google/design.md lint DESIGN.md`) into the project's own checks (CI or pre-commit) rather than running it once; for a project with no visual surface, don't mention the file or the linter at all.
- [ ] 6. Tell the user in one or two lines what changed, including any legacy project rules moved outside the markers. Say that records live under the folder and a human can explicitly vouch a line, section, or whole file with `[VOUCHED @<their-handle> YYYY-MM-DD]`. If records were seeded, say they are unstamped drafts awaiting review.

## Opening a decision ledger (on the user's declaration)

A decision ledger is opt-in and per-area: it exists only after the human declares that an area records decisions ("design decisions get recorded from now on"). When that happens, create `<area>-decisions.md` from the template below — next to the area's derived document when that document has a conventional home (`DESIGN-decisions.md` beside `DESIGN.md` at the repo root), otherwise in the records folder — and add a map route to it. You may suggest a ledger when an area's judgments grow dense; only the human's declaration creates one.

### The ledger template

```markdown
# <Area> decisions

Judgments the human actually expressed about <area> — selections, acceptances, rejections. A finished implementation, a passed review, resemblance to a reference, or the absence of an objection is not acceptance. Never invent a rationale: if no reason was given, the entry says so. Entries record the judgment, not the chosen thing's full content — details live in <the area's document>, linked. Edit entries in place; git keeps history.

## Decided

### <short stable topic>

[VOUCHED @handle YYYY-MM-DD]

- **Ruling:** <one plain sentence; its force in its own wording — must / never / prefer / default to>
- **Limits:** <what this does not govern; what may change without reopening it; what would reopen it>
- **Why:** <exactly as the human gave it; "no reason given" is honest>
- **Source:** <who, when, durable link; pin the accepted artifact (commit, section) when the ruling is "accept as reviewed">

## Open

### <short stable topic>

- **Question:** <what is undecided — current behavior is not a choice>
- **Holding:** <the stopgap, if any, and what would settle it>
```

The stamp line under a Decided heading appears only once the human vouches that entry — it covers the whole entry; a drafted entry starts without it.

## The block to inject

```
<!-- PCR:START -->
## Project Context Records (PCR)

This project follows **Project Context Records (PCR)** — methodology: https://github.com/hyfdev/project-context-records. PCR keeps the project's durable judgment — the *why*, the decisions, the intent — so you inherit it instead of re-deriving or re-litigating what's already settled.

When working here:
- **Where records live.** Records are in `.agents/docs/`, one topic per file, cross-linked with relative Markdown links.
  - A `README.md` there is the **map**: it routes code areas or hotspots to the exact record or heading, one-line gist per route. Create it when retrieval stops being a glance or one record grows into a long ledger.
- **Read first.** Start from the map if present, else scan the folder. Open the records or headings that cover an area before changing or answering for it; if the area has a decision ledger, read it first.
- **Use the strongest durable form.** Machine-checkable constraints go in types, tests, lints, or CI; single-spot rationale goes beside the code with a link; records carry the cross-cutting judgment, intent, and context that must stay prose.
- **Record as you go.** Capture context when a decision lands, a trap costs you, a human corrects you, or a human asks — anything true about this project, not durable in a stronger form, and useful beyond the moment.
  - Report what you record so a human can review or vouch it.
  - Records are as public as the repo: keep secrets out, and ask before recording rationale from private context.
- **Write to be acted on.** Lead with the current conclusion and where it applies; capture the why — trade-offs, alternatives rejected, known pitfalls. Keep each topic's current truth in one fresh place, updated in place: evolution belongs to git, never to supersede chains.
- **Keep it fresh.** Update affected records in the same change that touches their subject.
  - When code and a record disagree, decide which side went stale and fix that side.
  - Back facts with durable evidence — tests, reproducible commands, committed artifacts, stable URLs, commit hashes — not ephemeral paths or one session's output.
- **Provenance.** Unstamped text is AI-accumulated: challenge and verify it freely. `[VOUCHED @handle YYYY-MM-DD]` means the named human explicitly accepted the covered words as current project direction.
  - A vouch is direction, not proof: facts keep needing durable evidence. Don't reopen vouched direction for its own sake — only on new evidence, a changed constraint, or the human's say-so.
  - When evidence argues with vouched direction, record the conflict and surface it to a human; stay inside the direction unless progress becomes impossible. Silence is not an option.
  - Scope: at a non-heading line's end, the stamp covers that line; alone on the first nonblank line below a heading, that section until the next heading of the same or higher level; alone below the document title, the whole file. Never in heading text — link anchors derive from headings.
  - Add a stamp only on explicit instruction. A stamp added by work under review counts only once the named human confirms it; an unchanged stamp on the target branch is inherited project state.
  - The stamp binds the exact covered words. Any edit that changes them — or changes which words the scope covers — removes the stamp until the human re-vouches; a change that leaves the covered words identical keeps it.
  - Legacy stamp forms (undated, before the title, inside a heading) stay valid with their original scope; never move, re-date, or reinterpret one without the human's approval.
- **Decision ledgers.** When the human declares that an area records decisions, keep that area's judgments in `<area>-decisions.md` and register new judgments there.
  - Placement: beside the area's derived document when one has a conventional home (`DESIGN-decisions.md` beside `DESIGN.md`), else in the records folder — with a map route either way.
  - You may propose opening a ledger; only the human opens one.
  - The register contract: only judgments the human actually expressed enter — a finished implementation, a passed review, resemblance to a reference, or silence is not acceptance. Never invent a rationale: if no reason was given, the entry says so.
  - Record the act of judgment, not the chosen thing's full content — exhaustive detail lives in the area's own document, linked. Edit entries in place; git keeps history.
  - Entries sit under **Decided** or **Open**. An Open entry marks a known-undecided question — current behavior is not a choice — with any stopgap and what would settle it. A Decided entry carries:
    - a short stable topic heading — map routes and stamp scopes anchor to it;
    - **Ruling:** one plain sentence, its force in its own wording — must / never / prefer / default to; no status field;
    - **Limits:** what it does not govern, what may change without reopening it, what would reopen it — a stopgap is a ruling plus its reopen condition;
    - **Why:** premises, alternatives compared, rejections — exactly as the human gave them;
    - **Source:** who expressed it, when, a durable pointer; for "accept the reviewed thing as a whole", pin the thing (commit hash, spec section) instead of transcribing it;
    - the vouch stamp, once the human vouches the entry, alone under the entry's heading — covering the whole entry.
- **Distill when a human reviews.** Accumulation is noisy by design; the valve is a human pass, and you draft it.
  - Propose: prune what is contradicted or dead, merge near-duplicates, promote buried context, fix map drift. Unattended, apply this to your own unstamped layer as you go — never the vouched one.
  - Flag: unstamped direction that has become load-bearing, factual claims whose evidence no longer holds, vouches plausibly affected by changes to what they cover.
  - The human decides and vouches.
- **Suggested topics.** Draft the missing ones that apply; when an existing doc already covers a topic, enroll it — a map route pointing at it where it lives, held to these same rules — instead of drafting a twin:
  - `intent.md` — what this is trying to be, for whom, and the non-goals; enroll the README instead if it truly covers them.
  - `technology-stack.md` — why tools, restrictions, and pins exist; not a manifest dump.
  - `architecture.md` — units, boundaries, and why the lines are where they are; when structure isn't glanceable.
  - `gotchas.md` — traps already paid for, each with its why; only real paid lessons.
  - `DESIGN.md` — only for a visual surface; follow https://github.com/google-labs-code/design.md, keep it at the root, and enroll it in the map.
  - `loop-goal.md` — only for an unattended run: the run's contract — goal, boundaries, finish criteria — issued by the human (you may draft it; the human's go authorizes it). Never edit it mid-run; a human change to it re-baselines the run.
  - `loop-status.md` — only for an unattended run: the run's memory — done, in flight, next, blocked — overwritten in place each iteration; its final overwrite is the handover to the returning human (what landed, what to vouch, what to prune, conflicts included). Both `loop-*` files die after that distillation pass; git keeps them.
<!-- PCR:END -->
```
