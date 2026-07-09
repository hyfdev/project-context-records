# Project Context Records (PCR)

**English** · [简体中文](./README.zh-CN.md)

> A methodology for the AI era: keep a durable, repo-versioned archive of a project's **meta-context** — the *why*, the architecture, the maintainer decisions, the intent — so that an amnesiac, self-directed AI collaborator inherits the project's judgment instead of re-deriving it.
>
> It is also a harness: a way for a human to keep hold of the direction while the AI iterates fast.

PCR is a practice of **context engineering**. Context engineering curates what goes into a model's context; PCR is the project-scoped, persisted slice of that context — the part worth versioning, reviewing, and inheriting across sessions.

## TL;DR: How to use

**Recommended — install the setup skill once, globally:**

```
npx skills add hyf0/project-context-records -g
```

Then run `/pcr-setup` in any project to adopt PCR there — and re-run it anytime to update: it syncs the block to the latest version and never touches your records. The global install (`-g`) makes the command available across all your projects. (Skill installs are powered by [skills.sh](https://www.skills.sh).)

**Or do it by hand** — paste this block into your project's `AGENTS.md` / `CLAUDE.md` (point it at wherever you keep the records):

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

That block *is* the whole adoption. It routes every collaborator — human or agent — to the records and states the rules they must follow. It is deliberately thin: an agent automatically reads `AGENTS.md` every session but does **not** fetch URLs, so what's inlined is the every-session rules — plus the few bootstrap triggers that would otherwise never reach an adopted project (distill a map, start with the basic records); the rest stays one link away and never needs fetching for the agent to behave. The block also belongs to the methodology, not the project: re-running `/pcr-setup` overwrites it wholesale (only your records-folder path is carried over), so keep project-specific rules outside it — your records are never touched.

And it lives in `AGENTS.md` deliberately: that is the emerging cross-tool standard for agent instructions, so one file reaches every agent. Keep `CLAUDE.md` (and its cousins) as symlinks to it rather than parallel copies — the block, and everything else, lands everywhere at once. agents.md decides *which file agents read*; PCR is a methodology for *what goes in it and how it's maintained*.

Then just work: **accumulate** records freely as you go, and **distill** them — promoting the valuable, pruning the stale, stamping what a human vouches for — whenever a human reviews.

**Everything below is the *why*.** And the repo practices it: PCR's own records, map included, live in [`.agents/docs/`](./.agents/docs/) — read them as the worked example.

## Contents

- [The premise: output is bounded by context](#the-premise-output-is-bounded-by-context)
- [Why code is no longer enough](#why-code-is-no-longer-enough)
- [Keeping the wheel](#keeping-the-wheel)
- [Unattended runs](#unattended-runs)
- [Where it sits](#where-it-sits)
- [Building on ADR](#building-on-adr)
- [What goes in](#what-goes-in)
- [The starter set](#the-starter-set)
- [Finding the record: the map](#finding-the-record-the-map)
- [The mechanism: the provenance stamp](#the-mechanism-the-provenance-stamp)
- [Lifecycle: accumulate → distill](#lifecycle-accumulate--distill)
- [Writing conventions](#writing-conventions)

---

## The premise: output is bounded by context

An LLM's output is a function of its context. Give it the context that decides the answer and the result moves toward what the project wants; starve it and it fills the gap with confident guesses — which is where wrong-but-plausible work comes from.

The asymmetry is the point. More context has trade-offs (noise, diluted attention, tokens); *missing the context that decides the answer* has none — it just loses. A capable model reasoning without the deciding information still produces wrong work; its ceiling is set by what it can see.

This is why PCR has two halves: **accumulate** the judgment that would otherwise evaporate (too little is reliably bad), and **distill** it — pruning noise, keeping the current truth fresh (too much or stale is bad too).

---

## Why code is no longer enough

Code records the **result state**: what the system finally looks like. It structurally drops three things a collaborator needs:

1. **The rejected paths.** The code shows "we chose A," never "we considered B and C; B was killed because X." So the next collaborator sees A, asks "why not B?", tries B, and walks into the same wall.
2. **The status of a choice.** Is this a deliberate, closed decision, or a stopgap awaiting review? The code looks identical either way, but the two call for opposite actions.
3. **The provenance of a judgment.** On what constraints, trade-offs, and whose call did this rest? When the constraints change, the decision may need reopening — but only if you recorded what it was hanging on.

In the pre-AI era these lived in maintainers' heads and travelled by **continuity**: code review, mentorship, "ask the person who wrote it." Teams were continuous; the knowledge was tacit but unbroken.

An AI collaborator has **no continuity**. Every session is an amnesiac, capable, and *self-directed* newcomer. It does not "ask the person who wrote it" — it reasons, doubts, and acts on its own. Tacit knowledge is, to it, nonexistent. So the judgment layer that always existed but hid in human heads must now be made into an **explicit artifact** — or it re-evaporates, once per session, forever.

PCR is that artifact. What it preserves is not *what the code is*, but *how the judgment was reached* — so that thinking already paid for is not paid for again.

---

## Keeping the wheel

AI can iterate faster than any human can review. That forces a dilemma: review every step and you become the bottleneck, erasing the speed; review nothing and the work quietly drifts from what you wanted.

PCR is a way out. A human sets direction at a few durable points — the records they vouch for — and the AI runs fast within those rails. Control moves from reviewing every action, which doesn't scale, to owning the direction, which does. The vouched stamp is the steering input: a vouched call isn't re-opened each session without a real reason, so a decision you make once keeps shaping the work, session after session, instead of being re-argued every time.

So PCR is also a **harness**: a way to hand the AI execution speed while a human keeps the wheel. The scarce human act often shifts from doing the work, or checking it line by line, to setting and maintaining the direction the records encode.

---

## Unattended runs

The hardest test of PCR is a loop: an agent run in iterations — plan, build, test, fix, repeat — with no human between iterations. Each iteration starts amnesiac; nobody corrects mid-course. That is not a special case the methodology tolerates — it is its reader at maximum: amnesia at the highest frequency, self-direction with the least supervision. Three things change shape. (The agent's rules for this live in the block's **Unattended** bullet — the only text an adopted agent ever sees; this section is the why, and the human's half.)

**Before the loop, the human steers by vouching.** Direction that must survive a hundred iterations is written down before the first one and vouched: the goal record — what it's trying to be, and the non-goals — the architecture bets as `architecture.md` (a record born as a bet that matures into description), and hard constraints in the instructions file outside the block, where they fire every session. On a greenfield repo this direction *is* the seed; `pcr-setup` drafts it from your brief. From then on the standing rules do the steering: a vouched record is settled, and the loop may not re-litigate it. The stamp was built as the harness for exactly this — set the rails, then let go; and the boundary cuts both ways — what you leave unstamped, you delegate: unvouched ground is explicitly the loop's to decide and revise. If the loop finds evidence against a vouched call, it records the conflict for the human and stays inside the rails unless they make progress impossible; silence is the one thing it may not choose.

**During the loop, the records are the loop's memory — and the unstamped layer is its own to keep.** Iteration N+1 inherits iteration N's judgment through the records or not at all. Keep the current plan as one live record, overwritten in place as truth changes — the single-and-fresh rule applied to loop state; git keeps the trail. And because no human will prune for a while, the loop tidies its own unstamped layer — merges duplicates, deletes its dead notes, keeps the map honest. The vouched layer it never touches: tidying your own working memory claims no authority; editing a human's seal does.

**After the loop, the records are the audit trail.** The loop's exit act is the distillation draft: what was decided while you were gone, what it recommends vouching, what it proposes pruning, where reality argued with a vouched call. The returning human reads a diff of judgment, not two hundred transcripts — and the next run starts on distilled, partly-vouched ground.

One line does not move: **no amount of looping vouches anything.** A claim verified by fifty green runs is still AI-accumulated — strong evidence, and the prose should say so — but the stamp is not a measure of confidence; it is a human taking responsibility, and there is no human in the loop.

---

## Where it sits

```
Guiding philosophy   Context Engineering   — curate what's in the model's context
        └ Methodology   Project Context Records   — persist the project's slice of it
                └ Mechanism   the provenance stamp   — mark who stands behind a claim
```

---

## Building on ADR

PCR is the AI-era descendant of **Architecture Decision Records (ADR)** — a convention introduced by Michael Nygard in 2011 and since grown into an [ecosystem of tooling and templates][adr-hub]. An ADR records each significant decision as a small, numbered, version-controlled file stating its *context*, the *decision*, and its *consequences*; a decided record is never edited — to change it, you write a new one that **supersedes** it, leaving an append-only trail.

PCR keeps ADR's best instinct — *knowledge lives in the repo, reviewed and versioned with the code, not in a wiki* — and adapts it in three ways for the new reader:

1. **Decisions → context.** ADR centers one significant decision per file, with its context and consequences. PCR widens the unit to the whole meta-layer: decisions *and* architecture, mental models, deliberate divergences, gotchas, and in-flight plans. A decision is one slice of a project's context, not all of it.
2. **Immutable-and-stacked → single-and-fresh.** ADR preserves history by freezing each decided file and appending a new one that supersedes it; the current truth ends up scattered across that supersede chain. PCR keeps the **current conclusion in one fresh place** and lets **git** hold the evolution. An amnesiac agent re-reading a supersede chain to find today's answer is pure waste; give it one trustworthy answer and send history to the log. Rationale that still bears on the decision stays in the current entry; only the incidental evolution goes to git.
3. **Reader = human → reader = self-directed amnesiac agent.** ADR only describes, because a human reads the consequences and self-regulates. An agent will "discover" a settled thing and act on it. So a PCR entry may carry an **action directive to the agent** ("this is out of contract; don't re-flag it"), not just a description.

---

## What goes in

The **meta-layer** of a project: why it is shaped this way, the architecture, maintainer decisions, intent, deliberate divergences, mental models, hard-won gotchas, and plans currently in flight.

Negative definition, often sharper: **anything true about the project that the code can't tell you, and that stays useful beyond the moment.**

The same test runs against the project's agent-instructions file (`AGENTS.md`), from the other side. That file is **push** — every line lands in the model's context every session, needed or not; the records are **pull** — retrieved when the work touches them. So the instructions file earns its lines with a harder test: *must this be obeyed every session?* Everything that fails it but still matters — the why behind a rule, the architecture, the history, the gotchas — moves down into a record and is read when it's relevant. PCR is, among other things, the relief valve for the instructions file: the place its accumulating explanations were always trying to go.

Most repos already hold pieces of this layer — a `DESIGN.md` or `ARCHITECTURE.md` at the root, an `adr/` folder, internal docs. Those are records in every sense that matters: a record is defined by the rules it follows — kept fresh, stampable, reachable — not by the folder it sits in. **Enroll them**: give each a map row pointing at where it lives, hold it to the same rules, and don't migrate it — or worse, draft a twin that drifts against it. The records folder is the default home for what you write next, not a wall around what already exists.

Capture is **broad** — record anything plausibly useful, cheaply, as you go, ephemeral plans and in-flight reasoning included. Value is judged later, at **distillation** (below), not at capture time: what survives is the residue still useful beyond the moment. One boundary: records are exactly as public as the repo that holds them. What a human says in a session is not automatically publishable — keep secrets out, and when rationale rests on private context (unreleased plans, people, business constraints), ask before recording it.

---

## The starter set

"Record anything worth keeping" gives a new adopter no first move, and an empty records folder earns nothing on day one — which is exactly when an adopter decides whether the practice is worth keeping. A few topics, though, recur in nearly every project: the things an amnesiac collaborator wishes it knew on session one. Seed those at adoption instead of waiting for them to come up:

- **goal** — what the project is trying to be, for whom, and what it deliberately is not: the non-goals that keep scope honest. This is the most upstream judgment in the meta-layer — the intent everything else serves. Its home is a record, not the README: the README pitches to users; the goal record speaks to collaborators and holds what users don't need — the refusals, the priorities, the why. Where a README already states all of it, [enroll](#what-goes-in) it instead of writing a twin.
- **technology-stack** — what the project builds with, and the constraints around it. The list itself is already in the manifests; what earns the record is what they can't say: why these tools over the defaults they displaced, what must not be introduced, what is pinned and why. The record keeps the why; the one-line rules it justifies ("use pnpm", "never add X") are every-session material — they belong in the instructions file, which links here.
- **architecture** — the shape of the system as its maintainers hold it: the units, the boundaries between them, and why the lines are where they are.
- **conventions** — where this project deliberately departs from what the ecosystem would expect, so a departure reads as a decision, not as an accident a helpful newcomer should fix.
- **gotchas** — the traps already paid for: things that look safe and aren't, each with its why.

One more entry depends on the project's shape: **`DESIGN.md`**, for a project with a visual surface. It is the visual identity described to coding agents — machine-readable design tokens (colors, typography, spacing, components) in front matter, plus the prose why behind them — following the [design.md spec](https://github.com/google-labs-code/design.md). By that convention it lives at the repo root: [enroll](#what-goes-in) it in the map rather than moving it. Its ecosystem ships a linter (`npx @google/design.md lint DESIGN.md` — token references, WCAG contrast, schema keys); where the file exists, keep it lint-clean. A project with no visual surface skips the file and the linter entirely.

An agent can draft the applicable ones at adoption from the codebase, the manifests, and the git history — drafting only what existing docs don't already cover: a repo's existing `ARCHITECTURE.md` or `adr/` is [enrolled](#what-goes-in), not duplicated. The result is a first accumulation for a human to correct and, where it holds, vouch: day one ends with a reviewed skeleton instead of an empty folder.

These are prompts, not a schema: skip what doesn't apply, split what outgrows one file, rename freely. And the list grows the way everything in PCR grows — a topic joins it when real use keeps asking for it, not because it seems like it belongs.

---

## Finding the record: the map

Records only help if the reader opens the right one at the right moment. With a handful of files that is trivial — filenames are the index, and an agent can scan the folder and read what is short. At a few dozen it is not: an agent will not read every record each session, and "read the record that covers the area you're touching" quietly assumes the agent already knows which one that is. It doesn't. That gap — from the code in front of you to the record that bears on it — is the retrieval problem, and it is what separates a methodology that works at five records from one that still works at fifty.

The response is a **map** — but only once the folder needs one. When finding the right record stops being a glance — around a dozen files, or the moment enrolled records live outside the folder — distill a map: `.agents/docs/README.md`, each record listed once with the code area it covers and a one-line gist. Routing, not content — the content stays in the records; the map only points. From then on an agent starts at the map, matches the work in front of it — a change to make, or a question to answer — against it, and opens the records that cover it. "Read first" stops being a hope and becomes a lookup.

The map routes from the outside in; code can route from the inside out. Where a record explains something a stretch of code can't say for itself, leave a one-line comment at that spot pointing at the record (`// why: see .agents/docs/<topic>.md`). It fires exactly when someone — human or agent — is reading that code, which is sharper targeting than any index: the map covers areas, the breadcrumb covers the hot spot.

The map is itself a record, but a distilled one, never an accumulated one: you don't pour notes into it, you promote a line into it when a record earns its place. It can be vouched like any other — and a vouched map is a strong steering artifact, the maintainer's own index of what matters and where.

Its upkeep is the cheap kind of drift. A prose record rots invisibly — you learn it is wrong only by re-reading it against the code. The map rots on exactly two axes — a record present but unlisted, or a line pointing at a record that was renamed or removed — and both are caught by mechanically cross-checking the map against the folder. The expensive drift stays in the records; the map's is a lint.

And no map on day one, by design: a map over three records is ceremony — structure paid for before it returns anything. This is PCR's own rule applied to itself — structure is added when real use demands it, not ahead of it.

---

## The mechanism: the provenance stamp

This is the one piece of hard currency, and it rests on a first principle:

> In the AI era, text is cheap and **AI-authored by default**. The scarce, valuable act is a **human putting their seal on a claim.**

So the rule is a single bit:

- **No stamp = AI-accumulated.** The default substrate. Treat it as challengeable — question it, and verify it freely.
- **`[VOUCHED @handle]` = a human vouched for it.** Treat it as foundation: don't re-verify or reopen it for its own sake — do either only on new evidence, a changed constraint, or a human's say-so. A stamp marks a single line (at the end of it) or a whole file (at the top), and represents explicit human vouching: typed by a human, or added by an agent only on a human's explicit instruction. A human reading past a claim, or not objecting, never counts.

```
Timestamps are stored as UTC, converted only at the edges — settled after a DST bug.   [VOUCHED @hyf0]

Raising the cache TTL to 1h is probably safe.   ← no stamp: AI-accumulated, verify freely
```

**The stamp covers the words it sits on.** Materially editing a vouched line takes the stamp off until a human re-vouches it — otherwise an agent could reword the claim and leave new words wearing a seal no human gave them. Formatting-only changes keep it.

**The stamp carries a date.** `[VOUCHED @hyf0 2026-07-08]` records *when* the vouch was made. It is still the same one bit — a timestamp on it, not a new kind of stamp. What it buys is the question the bit alone can't answer: not just *did a human vouch*, but *is that vouch still current?* A `[VOUCHED]` from a year ago on a module rewritten twice since is the stale-record trap at its worst — settled-looking, and wearing a human seal. The date lets a [distillation pass](#lifecycle-accumulate--distill) flag it mechanically — stamp date against the code's last change — instead of by judgment call. And it is nearly free: most stamps are added by an agent on a human's instruction, and the agent knows the date — so an agent dates every stamp it adds. A human typing one by hand may skip the date; git can recover it later, but the reader shouldn't need archaeology, so date it when you think of it.

**The human seal is optional — for continuity, not for control.** The agent-accumulated substrate already carries the memory: an agent inherits what was recorded, vouched or not. What the seal adds is the harness from [Keeping the wheel](#keeping-the-wheel) — the human direction that holds across sessions. So vouch where the stakes justify it, and leave the rest as the honest default.

**Why a stamp, and only one kind.** The worst way an AI-maintained knowledge base fails is that the AI's own guesses get taken for facts a human has confirmed — a later agent treats a machine-made assumption as settled and builds on it. The stamp draws exactly that line, and only that line: **vouched for by a human, or not.** Finer distinctions — *decision or observation? settled or still tentative?* — belong in the entry's own text, not in more kinds of stamp. Start with this one; add more only if real use proves you need it.

---

## Lifecycle: accumulate → distill

- **Accumulate** (cheap, default, by agents): record context the moment it appears — a decision lands, a trap costs you, a human corrects you — and whenever a human asks; keep existing records fresh as your changes touch them. Volume is fine; noise is expected. Mention what you record — a human can't prune or vouch what they never see.
- **Distill** (scarce, human-owned): a review pass that **promotes** the valuable, **prunes** what's wrong or obsolete, and **vouches** for what holds — the vouch being the one part agents can't do. This is the human seal applied as a recurring practice, and where "implementation plans tracked temporarily" become "the valuable thing that remains."

Distillation is a human act, but it need not be a from-scratch one — and it shouldn't be, because human attention is the scarce thing PCR exists to conserve. A distillation pass that requires the busy maintainer to sit down and author a full review is a valve that rusts shut, and then the records grow into an unpruned, unvouched pile: noise with a folder. So the same self-directed agent that accumulates can **draft the distillation** — a pass over the records that produces the diff a human then approves, sorted into the moves a human is slow to find by hand:

- **contradicted** — records that no longer match the code they describe (found by re-reading each against its code);
- **redundant** — near-duplicate records that should merge;
- **buried** — valuable context sitting in an accumulated pile, worth promoting;
- **map drift** — records missing from the [map](#finding-the-record-the-map), or map lines pointing at records that moved;
- **load-bearing but unvouched** — unstamped claims that other records or code lean on, surfaced for a human to vouch or reject;
- **aging vouches** — vouched records whose code has changed since the stamp's date.

The agent drafts; the human approves, edits, and vouches in one pass. This is the [harness](#keeping-the-wheel) turned on the records themselves: the human still owns the direction, but distillation drops from *authoring* to *reviewing* — the difference between a practice that happens and one that stays a good intention. Nothing about *who vouches* changes: a stamp still counts only when a human adds it explicitly. Unattended — no human between iterations — the agent tidies the unstamped layer itself and queues the rest; see [Unattended runs](#unattended-runs).

---

## Writing conventions

- **One topic per file.** Cross-link related entries with standard relative Markdown links (`[other-topic](./other-topic.md)`) — clickable on GitHub, unambiguous, and tool-agnostic.
- **Once there is a [map](#finding-the-record-the-map), keep it complete.** A record no one can find is a record no one reads: when you add or rename one, update its map line in the same change.
- **Keep the current truth fresh.** Drift is the death risk: a confident record that no longer matches reality flips from asset to **trap** — an agent will act on it with full confidence. A stale record is worse than no record. When your change affects an entry, update the entry in the same change; when the code contradicts an entry, fix the entry — vouched ones excepted: surface that conflict to a human instead of silently overriding.
- **Capture the why**, not just the what: the trade-off, the alternatives rejected, the known pitfalls. Lead with the principle or intuition.
- **Write so a collaborator gets it without reading the code internals.** The entry stands on its own as prose; an agent reads it and *gets it*.
- **No fixed format — on purpose.** A record is just prose that conveys the why. A stricter shape may emerge from real use; don't impose one up front.

---

[adr-hub]: https://adr.github.io/
