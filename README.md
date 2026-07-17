# Project Context Records (PCR)

**English** · [简体中文](./README.zh-CN.md)

> Keep a project's judgment — the *why*, the decisions, the intent — as a versioned archive in the repo, so that an amnesiac AI collaborator inherits it instead of re-deriving it. And because the archive holds direction a human explicitly vouched for, it doubles as a harness: agents can run long and unattended while the human keeps the wheel.

## Contents

- [The idea](#the-idea)
- [Adopting PCR](#adopting-pcr)
- [Day to day: the context practice](#day-to-day-the-context-practice)
- [Loops: the unattended practice](#loops-the-unattended-practice)
- [The why](#the-why)
- [Where it sits](#where-it-sits)

## The idea

An LLM's output is a function of its context. What matters about that statement is its asymmetry: miss the one piece of context that decides an answer, and the work comes back wrong — confidently, plausibly wrong — and no amount of model capability compensates. More of the *right* context raises how good the work can get; missing the deciding piece caps it, hard.

The context that decides answers is mostly judgment, and code cannot carry it. Code records the result state — what the system finally looks like — and structurally drops the rest: which paths were rejected and why, whether a choice is a settled decision or a stopgap, and what a judgment rested on. That layer used to live in maintainers' heads and travel by continuity: code review, mentorship, "ask the person who wrote it." An AI collaborator has no continuity. Every session is an amnesiac, capable, self-directed newcomer, and tacit knowledge is, to it, nonexistent.

PCR is the practice of keeping that layer as an explicit artifact, versioned with the code:

- **Records** accumulate cheaply, in plain Markdown, as the work happens — no required format, no ceremony.
- A human **vouches** the records that should keep steering. One stamp, one bit — human-accepted direction, or challengeable AI notes. It is the methodology's only hard mechanism.
- **Distillation** keeps the archive worth reading: agents draft what to prune, merge, or promote; the human decides.
- Structure is **progressive**: named files, formats, and indexes appear when use demands them, never up front.

The same archive is also what makes long unattended runs steerable: the vouched records are the rails, the records are the loop's memory across iterations, and the run ends in a state the returning human can read. Context engineering is the guiding idea — what a model sees decides what it does. PCR is that idea practiced at project scale. Loops are where it pays off.

## Adopting PCR

**With the setup skill** (recommended):

```
npx skills add hyfdev/project-context-records -g
```

Then run `/pcr-setup` in any project. To update an adopted project later, refresh the skill first, then re-run it:

```
npx skills update pcr-setup -g
```

`npx skills` fetches the latest methodology; running `/pcr-setup` in the project applies it. (Skill installs are powered by [skills.sh](https://www.skills.sh).)

**Or by hand:** paste the block below into the project's `AGENTS.md`, pointing the "Where records live" bullet at your records folder if it differs from the default.

The block is the **entire adoption surface**. An adopted project's agents read `AGENTS.md` every session and never fetch this repo: what must reach them is in the block, and everything else here is for humans. It therefore optimizes for completeness, not brevity — every rule an agent must follow lives in it, at full strength, because no other channel exists. Everything it names — the map, the stamp, decision ledgers, the loop files — is explained in the chapters that follow. It lives in `AGENTS.md` deliberately — the emerging cross-tool standard for agent instructions — so one file reaches every agent; keep `CLAUDE.md` and its cousins as symlinks to it. The markers bound ownership: re-running `/pcr-setup` replaces only the text between `<!-- PCR:START -->` and `<!-- PCR:END -->`, carries your records-folder path over, and never modifies existing records — its only record-side acts, seeding drafts into an empty folder and renaming a legacy `goal.md` to `intent.md`, each happen only on your approval. Project-specific rules live outside the markers.

```
<!-- PCR:START -->
## Project Context Records (PCR)

This project follows **Project Context Records (PCR)** — methodology: https://github.com/hyfdev/project-context-records. PCR keeps the project's durable judgment — the *why*, the decisions, the intent — so you inherit it instead of re-deriving or re-litigating what's already settled.

When working here:
- **Where records live.** Records are in `.agents/docs/`, one topic per file, cross-linked with relative Markdown links.
  - A `README.md` there is the **map**: it routes code areas or hotspots to the exact record or heading, one-line gist per route. Create it when retrieval stops being a glance or one record grows into a long ledger.
- **Read first.** Start from the map if present, else scan the folder. Open the records or headings that cover an area before changing or answering for it; if the area has a decision ledger, read it first.
- **Use the strongest durable form.** Machine-checkable constraints go in types, tests, lints, or CI; rules that must bind every session go in the agent-instructions file, outside the markers; single-spot rationale goes beside the code with a link; records carry the cross-cutting judgment, intent, and context that must stay prose.
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
  - Placement: beside the area's derived document (`DESIGN-decisions.md` beside `DESIGN.md`); with no derived document, in the records folder — a map route either way.
  - You may propose opening a ledger; only the human opens one.
  - The register contract, stated at the top of the file: only judgments the human actually expressed enter — a finished implementation, a passed review, resemblance to a reference, or silence is not acceptance. Never invent a rationale: if no reason was given, the entry says so.
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
  - `DESIGN.md` — only for a visual surface; follow https://github.com/google-labs-code/design.md (repo root by default — the spec fixes no location), enroll it in the map, and suggest wiring its linter into the project's own checks (`npx @google/design.md lint DESIGN.md`; platform variants in the spec).
  - `loop-goal.md` — only for an unattended run: the run's contract — goal, boundaries, finish criteria. You may draft it; the run starts only once the human has vouched the whole file (stamp below the title), and a human edit plus re-vouch re-baselines it. Never edit it yourself; if the contract itself blocks progress, stop and surface the conflict rather than stepping outside it.
  - `loop-status.md` — only for an unattended run: the run's memory — done, in flight, next, blocked — overwritten in place each iteration; its final overwrite is the handover to the returning human (what landed, what to vouch, what to prune, conflicts included). Both `loop-*` files die after the human's distillation pass over that handover; git keeps them.
<!-- PCR:END -->
```

Then just work: accumulate freely, distill when you review, vouch what should keep steering.

## Day to day: the context practice

### Records: the free base

Records live in the repo — `.agents/docs/` by default — one topic per file, cross-linked with relative Markdown links. A record is prose that carries the why; there is no required format.

What earns a record: anything true about the project that the code alone cannot say, that no stronger home fits, and that stays useful beyond the moment — decisions with their rejected alternatives, architecture rationale, deliberate divergences from ecosystem defaults, traps already paid for, plans in flight.

"No stronger home" is a real test, applied first:

- Machine-checkable constraints go in types, tests, lints, or CI. A record may explain why the constraint exists; it is not the enforcement.
- Rationale that matters at one code hotspot goes beside that code, with a link out when the full reasoning is bigger than a comment.
- Temporary execution state goes in an issue or one live, replaceable plan.
- What remains for records: cross-cutting judgment, intent, and context that must stay prose.

The same test runs against the agent-instructions file (`AGENTS.md`) from the other side. That file is push — every line lands in the model's context every session, needed or not. Records are pull — read when the work touches them. So the instructions file earns its lines against a harder bar (*must this be obeyed every session?*), and everything that fails that bar but still matters moves down into a record. PCR is also the relief valve for the instructions file.

Capture is broad and cheap: record when a decision lands, when a trap costs you, when a human corrects you, or when a human asks. Keep records fresh in the same change that touches their subject — a stale record is worse than none, because an agent acts on it with full confidence. When code and a record disagree, decide which side went stale and fix that side; when the record is vouched, surface the conflict to a human instead of silently overriding it. Keep evidence durable: tests, reproducible commands, committed artifacts, stable URLs, commit hashes — not temporary paths or one session's output.

Two boundaries. Records are exactly as public as the repo that holds them: keep secrets out, and when rationale rests on private context, ask before recording it. And repos that already hold pieces of this layer — a root `ARCHITECTURE.md`, an `adr/` folder, internal docs — **enroll** those where they live, with a map route pointing at the exact file or heading (see [The map](#the-map)), instead of migrating them or drafting twins that drift against them.

### Suggested topics

A blank folder gives no first move. These names remove the "what file do I create" overhead; each carries the condition under which it applies, and skipping is normal. They are prompts, not a schema:

- **`intent.md`** — what this project is trying to be, for whom, and the non-goals that keep scope honest. Nearly every project; if the README truly covers it, enroll the README instead — it usually pitches to users, while intent speaks to collaborators.
- **`technology-stack.md`** — why these tools over the defaults they displaced, what must not be introduced, what is pinned and why. When tool judgment exists; never a manifest dump.
- **`architecture.md`** — the units, the boundaries between them, and why the lines are where they are. When the structure stops being glanceable from the code.
- **`gotchas.md`** — traps already paid for, each with its why. Only real paid lessons; better no file than invented "common pitfalls".
- **`DESIGN.md`** — only for a project with a visual surface: its visual identity described for coding agents, per the [design.md spec](https://github.com/google-labs-code/design.md) — enrolled in the map, with that ecosystem's own linter available for the project's checks. The spec fixes no location; the repo root is the usual home.

### The map

Records only help if the right one is opened at the right moment. While the folder is small, filenames are the index. Once retrieval stops being a glance — many files, a long ledger, enrolled records outside the folder — distill a **map**: `.agents/docs/README.md`, routing each code area or hotspot to the exact record or heading, with a one-line gist per route. The map routes; content stays in the records. And it is a record like any other: adding or renaming a routed record updates the map in the same change. For a narrow hotspot, a one-line breadcrumb in the code (`// why: see .agents/docs/<topic>.md#<heading>`) fires at exactly the right moment. No map on day one — a map over three short records is ceremony.

### The stamp

In an AI-maintained archive, text is cheap and AI-authored by default. The scarce act — the one thing only a human can add — is explicitly taking responsibility for direction. The stamp is that act, and it is one bit:

- **No stamp** — AI-accumulated. The default substrate: challenge it, verify it, rewrite it freely.
- **`[VOUCHED @hyfdev 2026-07-08]`** — the named human explicitly accepted the covered words as current project direction. Treat it as foundation: don't reopen it for its own sake — reopen on new evidence, a changed constraint, or the human's say-so.

A vouch is about direction, not truth. It does not make a factual claim proven; facts keep needing durable evidence. The date records when the human last accepted the direction — age you can see, not freshness you can assume.

Scope, in one breath: at the end of a line, the stamp covers that line; alone on the first nonblank line below a heading, that section; alone below the document title, the whole file. It never goes inside heading text, because link anchors derive from headings. Editing the covered words takes the stamp off until the human re-vouches — only a change that leaves them identical keeps it; otherwise an agent's new words would wear a seal no human gave them. The full operating rules an agent needs — when a new stamp counts, how legacy stamps are treated — travel in the [adoption block](#adopting-pcr), not here.

Why only one kind of stamp: the worst failure of an AI-maintained archive is the AI's own proposal being mistaken for direction a human accepted, and then built upon. The stamp draws exactly that line — explicitly accepted, or not. Finer distinctions (decision or observation, settled or tentative) belong in an entry's own text. Start with one bit; add more only if real use proves the need.

### Decision ledgers

Some areas collect human judgment as a stream — selections, acceptances, rejections, call after call across many sessions of review — while an AI synthesizes the results into specs and implementation. Those judgments deserve a registry that the syntheses can be checked against. That registry is the area's **decision ledger**: `<area>-decisions.md`.

A ledger is **opt-in and per-area**. It exists only after the human declares that the area records decisions ("design decisions get recorded from now on"). An agent that notices judgment-dense traffic may propose opening one; only the human opens it.

Its defining discipline is the **register contract**, stated at the top of the file: only judgments the human actually expressed may enter. A finished implementation, a passed review, resemblance to a reference, or the absence of an objection is not acceptance. And a rationale is never invented: if the human gave no reason, the entry says so.

Entries sit in two zones — **Decided**, and **Open** for the known-undecided. An Open entry marks that current behavior is not a choice — exactly the thing an agent cannot otherwise tell — and carries the question, plus any stopgap and what would settle it. A Decided entry keeps a basic shape, free within it:

- a short, **stable topic heading** — stable because map routes and stamp scopes anchor to it;
- the **ruling**, first: one plain sentence, its force in its own wording — *must*, *never*, *prefer*, *default to*. There is no status field to restate what the sentence already says;
- its **limits** — what it does not govern, what may change without reopening it, and what would legitimately reopen it. A stopgap is not a special state: it is a ruling plus its reopen condition;
- the **why** — premises, alternatives compared, rejections — exactly as given;
- the **source** — who expressed it and when, with a durable pointer when one exists. When the decision was "accept the reviewed thing as a whole", pin the thing — a commit hash, a spec section — instead of transcribing it.

When the human vouches an entry, the stamp sits alone under the entry's heading, covering the whole entry — so an edit to any covered part takes the stamp off until the human re-vouches.

One length discipline keeps a ledger from bloating into a second spec: **it records the act of judgment, not the content of what was chosen.** Exhaustive parameters live in the area's own document, linked from the entry.

There is no superseded state. When a ruling changes, edit the affected entries in place, in the same change; git keeps the evolution.

A ledger often stands **paired** with a derived document that an AI keeps current: the ledger holds what the human ruled; the document holds the synthesized present truth, checkable against the ledger. The visual instance of the pairing is `DESIGN-decisions.md` beside `DESIGN.md`. A ledger lives next to its derived document; with no derived document, it lives in the records folder. Either way, the map routes to it.

For a real, public ancestor of this pattern, see [musubi's `DESIGN-decisions.md`](https://github.com/hyfdev/musubi/blob/v2/DESIGN-decisions.md) — the file the ledger was promoted from. It predates the format above, and the drift visible in it — a five-value status vocabulary that collapsed in practice to one value, entries swelling into spec detail, a self-invented format section at the bottom of the file — is exactly why the format exists.

### Accumulate → distill

- **Accumulate** — cheap, default, agent-done. Record as you go, keep records fresh, and mention what you recorded — a human can't prune or vouch what they never see. Noise is expected; volume is fine.
- **Distill** — the valve, human-owned but agent-drafted. The agent drafts a reviewable pass over the records: what to prune, what to merge, what to promote; which vouches are plausibly aging; which unstamped direction has become load-bearing; which factual claims lost their evidence. The human edits, decides — and vouches only what they explicitly accept. Distillation is where "notes tracked along the way" becomes "the thing that remains".

## Loops: the unattended practice

The hardest reader PCR serves is not a session but a run: an agent iterating — plan, build, test, fix — with no human between iterations. Amnesia at its highest frequency, supervision at its lowest. It is also where the practice pays off most: the human present at the decisions, absent from the labor.

Two files carry a run, both under the `loop-` prefix. The prefix is a lifecycle marker: `loop-*` files are born when a run starts and die after its distillation — run-scoped state, visibly separate from the project-scoped records they sit among. Git keeps their history.

- **`loop-goal.md` — the contract.** What this run must accomplish, its boundaries, its finish criteria. An agent may draft it, but the run starts only once the human has vouched the whole file — the contract is vouched direction, carried by the same stamp as everything else, not a second authorization channel. **The loop never edits its own contract.** Only the human changes it, and a changed, re-vouched contract re-baselines the run; if the contract itself blocks progress, the loop stops and surfaces the conflict instead of stepping outside it.
- **`loop-status.md` — the memory.** Done, in flight, next, blocked — overwritten in place every iteration: one file, always current. Iteration N+1 inherits iteration N through this file and the records, or not at all.

The kickoff can then be one line — *execute the contract in `loop-goal.md`* — because the file, not the prompt, is the authority. Any driver that can re-invoke an agent can run the same loop.

A run has three acts:

**Before, the human steers by vouching.** Direction that must survive a hundred iterations is written and vouched before the first: `intent.md`, the architecture bets, the rulings in any active ledgers, and the contract itself in `loop-goal.md` — with hard every-session rules in the instructions file and machine-checkable constraints in CI, each in its stronger home. The boundary cuts both ways: vouched records are direction the loop may not re-litigate, and what stays unstamped is explicitly delegated — the loop's to decide and revise.

**During, the records are the only memory.** The loop reads them, keeps them fresh, and tidies its own unstamped layer — merging duplicates, pruning dead notes — while never touching the vouched one. When evidence argues with vouched direction, it records the conflict and stays inside the direction unless progress becomes impossible; silence is the one choice it does not have.

**After, the exit is a view for the returning human.** The run's last act is overwriting `loop-status.md` into a handover: what landed, what deserves a vouch, what to prune, and where reality argued with a vouched call. That final overwrite is the distillation draft in file form — the returning human reads a diff of judgment, not two hundred transcripts. There is no separate handover artifact; the memory's final state is the handover.

No run, however long or green, vouches anything. Verification is evidence about claims — worth recording. The stamp is a human taking responsibility, and it waits for one.

One checkout runs one loop; parallel runs live in separate worktrees.

The run shape these files were distilled from is public: [musubi](https://github.com/hyfdev/musubi) was rebuilt this way — the human's part was a few dozen ledger rulings and the go; the agent's part was everything in between, across long unattended stretches, with the records as memory and an exit state for each return.

## The why

### Why code is no longer enough

The idea above named the diagnosis in a sentence; here it is concretely. Code keeps the result state and drops three things a collaborator needs:

1. **The rejected paths.** Code shows "we chose A" — never "B and C were considered; B died because X." The next collaborator sees A, asks "why not B?", tries B, and walks into the same wall.
2. **The status of a choice.** A deliberate, closed decision and a stopgap awaiting review look identical in code — and they call for opposite actions.
3. **What a judgment rested on.** Constraints change. Whether a decision should be reopened depends on what it was hanging on — recoverable only if someone recorded it.

Pre-AI, the lost layer still worked because teams were continuous: review, mentorship, and asking the author kept tacit knowledge unbroken. An AI collaborator breaks the chain — and it does not ask; it reasons, doubts, and acts on its own. So the judgment layer that always existed must become an explicit artifact, or it re-evaporates, once per session, forever.

### Keeping the wheel

AI iterates faster than any human can review. Review every step and you become the bottleneck, erasing the speed; review nothing and the work quietly drifts from what you wanted. PCR's answer: the human sets direction at a few durable points — the vouched records — and the AI runs fast within them. Control moves from reviewing every action, which does not scale, to owning the direction, which does. A decision vouched once keeps shaping the work, session after session, instead of being re-argued every time.

### Building on ADR

PCR descends from [Architecture Decision Records][adr-hub] — Michael Nygard's 2011 convention: each significant decision as a small, numbered, version-controlled file; a decided record never edited, only superseded by a newer one, leaving an append-only trail. PCR keeps ADR's best instinct — knowledge lives in the repo, reviewed and versioned with the code, not in a wiki — and changes four things for the new reader:

1. **Decisions → context.** ADR records decisions. PCR widens the unit to the whole judgment layer: architecture, mental models, deliberate divergences, gotchas, intent, plans in flight.
2. **Immutable-and-stacked → single-and-fresh.** An amnesiac agent re-reading a supersede chain to find today's answer is pure waste. PCR keeps the current conclusion in one fresh place; git holds the evolution.
3. **Reader = human → reader = self-directed amnesiac agent.** ADR only describes, because a human reads the consequences and self-regulates. An agent will "discover" a settled thing and act on it — so a record may carry an action directive ("deliberately out of scope; don't re-flag it"), not just description.
4. **The decision file returns, transformed.** Where judgment about one area arrives as a stream, PCR's decision ledger is the ADR idea reshaped by the first three changes: per-area rather than per-decision, edited in place rather than superseded, and registering the judgments a human actually expressed rather than documenting every choice made.

### Progressive by design

PCR adds structure only when use demands it. The layers, in order of appearance:

1. **The free base** — always on: record anything, however you like, in plain prose.
2. **Suggested topics** — names that remove the first-move overhead, each with its applicability condition.
3. **Opt-in patterns** — the decision ledger (on the human's declaration), the design pairing (visual surface), the map (when retrieval stops being a glance), the `loop-*` files (when a run starts). Each arrives with the minimum format that real use proved necessary — and the format ships with the file, not as an up-front rulebook.
4. **Promotion** — the growth mechanism itself: a pattern that keeps recurring in real projects gets promoted into a suggested topic or an opt-in pattern. The decision ledger began as one project's `DESIGN-decisions.md`. Nothing enters because it would be nice; see [CONTRIBUTING](./CONTRIBUTING.md).

And the whole spec stays prose. Adoption is pasting one block; nothing in PCR requires software — no required CI, bots, parsers, front matter, or schema. Standards spread by being trivially adoptable — ADR, Conventional Commits, semver — and every mechanism added to a spec taxes that. Tools may consume records, the way adr-tools consumes ADR, without the convention ever depending on them.

## Where it sits

```
Guiding idea    Context Engineering — what a model sees decides what it does
    └ Methodology    Project Context Records — the project's slice: persisted, versioned, vouched
            └ Mechanism    the provenance stamp — the one bit only a human can add
```

Loop engineering — running the unattended loops above — sits on top, as the payoff: runs steered by the vouched layer, remembered through the records.

[adr-hub]: https://adr.github.io/
