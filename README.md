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

Then run `/pcr-setup` in any project to adopt PCR there. The global install (`-g`) makes the command available across all your projects. (Skill installs are powered by [skills.sh](https://www.skills.sh).)

When you later update an adopted project, refresh the installed skill before asking it to apply the latest block:

```
npx skills update pcr-setup -g
```

Then run `/pcr-setup` in the project. Updating the skill fetches the latest methodology; running it applies that version to the project.

**Or do it by hand** — paste this block into your project's `AGENTS.md` / `CLAUDE.md` (point it at wherever you keep the records):

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

That block *is* the whole adoption. It routes every collaborator — human or agent — to the records and states the rules they must follow. Its scope is deliberately bounded: an agent automatically reads `AGENTS.md` every session but does **not** fetch URLs, so what's inlined is the every-session rules — plus the few bootstrap triggers that would otherwise never reach an adopted project (distill a map, start with the basic records); the rest stays one link away and never needs fetching for the agent to behave. The marked block belongs to the methodology, not the project: after the skill is updated, re-running `/pcr-setup` replaces only the text between `<!-- PCR:START -->` and `<!-- PCR:END -->`, carrying over the records-folder path. Keep project-specific rules outside the markers. On a legacy unmarked block, setup first moves clear project-specific additions outside the new markers instead of deleting them; if old methodology and a possible local edit cannot be separated confidently, it stops and shows the proposed split for confirmation. Your records are never touched.

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

The hardest test of PCR is a loop: an agent run in iterations — plan, build, test, fix, repeat — with no human between them. It is the methodology's reader at its most extreme — amnesia at the highest frequency, the least supervision — and PCR is what makes such a run steerable and auditable.

**Before** the loop, the human records and vouches the direction — the goal and architecture bets — while hard every-session instructions and machine-checkable constraints live in their stronger repository homes: vouched records are direction the loop may not re-litigate, and what stays unstamped is explicitly delegated to the loop. **During**, the records are the loop's prose memory across iterations, and it maintains its own unstamped layer while never touching the vouched one. **After**, the records are the audit trail: the loop exits by drafting the distillation, so the returning human reads a diff of judgment, not two hundred transcripts. And no amount of looping vouches anything — verification is evidence for the prose; the stamp waits for a human. The agent-side rules live in the block's **Unattended** bullet; the full reasoning is in [unattended-runs](./.agents/docs/unattended-runs.md).

---

## Where it sits

```
Guiding philosophy   Context Engineering   — curate what's in the model's context
        └ Methodology   Project Context Records   — persist the project's slice of it
                └ Mechanism   the provenance stamp   — mark direction a human explicitly accepts
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

Negative definition, often sharper: **anything true about the project that is not already durable in a stronger form, that the code alone cannot tell you, and that stays useful beyond the moment.**

PCR is not the first home for every constraint. If a machine can check it, encode it in a type, test, lint, or CI gate and let the record explain only the rationale and when to reconsider it. Put rationale that matters at one code hotspot beside that code, with a link to deeper context when needed. Use an issue or one replaceable live plan for temporary execution state. PCR is for cross-cutting judgment, intent, and other context that still needs prose ([records and enforcement](./.agents/docs/records-vs-enforcement.md)).

The same test runs against the agent-instructions file (`AGENTS.md`), from the other side. That file is **push** — every line lands in the model's context every session, needed or not; records are **pull** — read when the work touches them. So the instructions file earns its lines with a harder test — *must this be obeyed every session?* — and everything that fails it but still matters moves down into a record. PCR is also the relief valve for the instructions file.

Most repos already hold pieces of this layer — a root `ARCHITECTURE.md` or `DESIGN.md`, an `adr/` folder, internal docs. Those are already records — **enroll them** with a map route to the exact file or heading, held to the same rules — instead of migrating them, or drafting twins that drift against them ([existing-docs](./.agents/docs/existing-docs.md)).

Capture is **broad** — record anything plausibly useful, cheaply, as you go, ephemeral plans and in-flight reasoning included. Value is judged later, at **distillation** (below), not at capture time: what survives is the residue still useful beyond the moment. Evidence meant to survive must survive with the record: prefer tests, reproducible commands, committed artifacts, stable URLs, and commit hashes over temporary files or one session's output. One boundary: records are exactly as public as the repo that holds them. What a human says in a session is not automatically publishable — keep secrets out, and when rationale rests on private context (unreleased plans, people, business constraints), ask before recording it.

---

## The starter set

"Record anything worth keeping" gives a new adopter no first move, and an empty records folder earns nothing on day one — exactly when an adopter decides whether the practice is worth keeping. So the block recommends a starting list, **the basics**: `goal.md` (what this is trying to be, for whom, and the non-goals), `technology-stack.md`, `architecture.md`, `conventions.md`, `gotchas.md`, and — for a project with a visual surface — a root `DESIGN.md` in the [design.md](https://github.com/google-labs-code/design.md) format. Each holds what nothing else can say — a goal record keeps the intent and refusals a user-facing README won't carry; a stack record keeps the whys the manifest can't — and the per-topic reasoning lives in [starter-set](./.agents/docs/starter-set.md).

`/pcr-setup` seeds the applicable ones at adoption — drafted from the codebase and history, or from your brief on a greenfield repo — for a human to correct and vouch: day one ends with a reviewed skeleton instead of an empty folder. These are prompts, not a schema: skip what doesn't apply, split what outgrows one file, rename freely. And the list grows the way everything in PCR grows — a topic joins when real use keeps asking for it.

---

## Finding the record: the map

Records only help if the reader opens the right part at the right moment. With a handful of short files, filenames are the index; once files or individual ledgers grow, an agent no longer reads everything and starts to guess. That gap — from the work in front of you to the exact record or heading that bears on it — is the retrieval problem.

The answer is a **map**, but only once retrieval needs one: when finding the exact context stops being a glance, when one record becomes a long ledger, or when enrolled records live outside the folder. Distill `.agents/docs/README.md` so each route names the code area or hotspot, links the exact record or heading, and gives a one-line gist. A dense record can appear through multiple heading links; routing, not content. Code can also route back the other way: a one-line comment at a hot spot (`// why: see .agents/docs/<topic>.md#heading`) fires exactly when someone is reading that code — the map covers areas, the breadcrumb covers the spot.

Why a map file rather than co-location or scope-tags, why none on day one, and how routes stay current are recorded in [the-map](./.agents/docs/the-map.md).

---

## The mechanism: the provenance stamp

This is the one piece of hard currency, and it rests on a first principle:

> In the AI era, text is cheap and **AI-authored by default**. The scarce, valuable act is a **human explicitly taking responsibility for project direction.**

So the rule is a single bit:

- **No stamp = AI-accumulated.** The default substrate. Treat it as challengeable — question it, and verify it freely.
- **`[VOUCHED @handle 2026-07-08]` = the named human explicitly accepts the covered words as current project direction.** Treat that direction as foundation: don't reopen it for its own sake — do so only on new evidence, a changed constraint, or a human's say-so. A vouch is not proof that an empirical claim is true; keep durable evidence for facts and recheck it when the work depends on it. Put the stamp at the end of a non-heading line for that line, as the first nonblank line below a non-title heading for that section, or as the first nonblank line below the document title for the whole file. Never put a new stamp in heading text: changing that text breaks map anchors. A human reading past text or not objecting never counts. A stamp added by the current change is only a claim until the named human explicitly confirms it; an unchanged stamp already on the target branch is inherited project state. Legacy undated stamps remain vouched, but gain a date only when a human re-vouches.

```
Timestamps are stored as UTC, converted only at the edges — settled after a DST bug.   [VOUCHED @hyf0 2026-07-08]

Raising the cache TTL to 1h is probably safe.   ← no stamp: AI-accumulated, verify freely
```

**The stamp covers exactly one declared scope.** Materially editing a vouched line, section, or file takes the stamp off until a human re-vouches it — otherwise an agent could reword the direction and leave new words wearing a seal no human gave them. A heading-level change, inserted or removed boundary heading, moved stamp, or line rewrap is also material whenever it changes which words the stamp covers; a formatting-only change keeps the stamp only if the covered set is identical. The position disambiguates a standalone stamp: the first nonblank line below the document title means the file; the first nonblank line below any other heading means that section until the next heading of the same or higher level. Legacy standalone stamps before the title remain whole-file vouches. A legacy stamp in heading text keeps any scope the project already declared; if that scope is undocumented, preserve its prior interpretation and surface the ambiguity when work depends on it. Never move or reinterpret a legacy stamp until the named human re-vouches or explicitly approves the migration.

**The date makes age visible, not freshness automatic.** It is the same one bit, timestamped — not a new kind of stamp — and tells a reviewer when the direction was last vouched. The date alone cannot identify which code it covers or prove that the words are still true; map routes, code breadcrumbs, durable evidence, and a [distillation pass](#lifecycle-accumulate--distill) make that comparison possible ([freshness](./.agents/docs/freshness.md)).

**The human seal is optional for memory, but necessary for explicit human direction.** The agent-accumulated substrate already carries memory: an agent inherits what was recorded, vouched or not. What the seal adds is the harness from [Keeping the wheel](#keeping-the-wheel) — direction a human deliberately holds across sessions. So vouch where the stakes justify it, and leave the rest as the honest default.

**Why a stamp, and only one kind.** The worst way an AI-maintained knowledge base fails is that the AI's own proposal gets taken for direction a human accepted — a later agent treats a machine-made assumption as settled and builds on it. The stamp draws exactly that line, and only that line: **explicitly accepted by a human, or not.** It does not replace factual evidence. Finer distinctions — *decision or observation? settled or still tentative?* — belong in the entry's own text, not in more kinds of stamp. Start with this one; add more only if real use proves you need it.

---

## Lifecycle: accumulate → distill

- **Accumulate** (cheap, default, by agents): record context the moment it appears — a decision lands, a trap costs you, a human corrects you — and whenever a human asks; keep existing records fresh as your changes touch them. Volume is fine; noise is expected. Mention what you record — a human can't prune or vouch what they never see.
- **Distill** (scarce, human-owned): a review pass that **promotes** the valuable, **prunes** what's wrong or obsolete, and asks a human to **vouch** for direction that should keep holding — the vouch being the one part agents can't do. Facts remain supported by durable evidence. This is where "implementation plans tracked temporarily" become "the valuable thing that remains."

Distillation is a human act, but not a from-scratch one — human attention is the scarce thing PCR exists to conserve, and a pass that demands authored reviews is a valve that rusts shut. So the same agent that accumulates **drafts the distillation**: a reviewable diff proposing what to prune, merge, or promote, plus plausibly aging vouches, load-bearing-but-unvouched direction, and factual claims whose durable evidence no longer holds — the full taxonomy is in [distill-draft](./.agents/docs/distill-draft.md). The human approves and edits the draft, then vouches only the direction they explicitly accept. Unattended, the agent tidies only the unstamped layer and queues the rest; see [Unattended runs](#unattended-runs).

---

## Writing conventions

- **One topic per file.** Cross-link related entries with standard relative Markdown links (`[other-topic](./other-topic.md)`) — clickable on GitHub, unambiguous, and tool-agnostic. A long ledger starts with a compact route to its important headings.
- **Once there is a [map](#finding-the-record-the-map), keep its routes complete.** Context no one can find is context no one reads: when you add or rename a record or a routed heading, update the map in the same change.
- **Keep the current truth fresh.** Drift is the death risk: a confident record that no longer matches reality flips from asset to **trap** — an agent will act on it with full confidence. A stale record is worse than no record. When code and a record disagree, decide whether the implementation drifted from intended direction or the description went stale, then update the stale side. Surface a vouched conflict to a human instead of silently overriding it.
- **Keep evidence durable.** A test, reproducible command, committed artifact, stable URL, or commit hash can support a later audit. A `/tmp` path, missing screenshot, or one-off session result cannot; label it as a temporary observation or preserve the artifact.
- **Capture the why**, not just the what: the trade-off, the alternatives rejected, the known pitfalls. Lead with the principle or intuition.
- **Write so a collaborator can act without reading the whole codebase.** Lead with the current conclusion and where it applies; include the reason, evidence, and conditions that would reopen it when those matter.
- **No fixed format — on purpose.** A record is just prose that conveys the why. A stricter shape may emerge from real use; don't impose one up front.

---

[adr-hub]: https://adr.github.io/
