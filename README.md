# Project Context Records (PCR)

**English** · [简体中文](./README.zh-CN.md)

> A methodology for the AI era: keep a durable, repo-versioned archive of a
> project's **meta-context** — the *why*, the architecture, the maintainer
> decisions, the intent — so that an amnesiac, self-directed AI collaborator
> inherits the project's judgment instead of re-deriving it.
>
> It is also a harness: a way for a human to keep hold of the direction while the
> AI iterates fast.

PCR is a practice of **context engineering**. Context engineering curates what
goes into a model's context; PCR is the project-scoped, persisted slice of that
context — the part worth versioning, reviewing, and inheriting across sessions.

## TL;DR: How to use

Paste this block into your project's `AGENTS.md` / `CLAUDE.md` (point it at
wherever you keep the records):

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

That block *is* the whole adoption. It routes every collaborator — human or agent —
to the records and states the rules they must follow. It is deliberately thin: an
agent automatically reads `AGENTS.md` every session but does **not** fetch URLs, so
only what must be obeyed every session is inlined; the rest stays one link away and
never needs fetching for the agent to behave.

Then just work: **accumulate** records freely as you go, and **distill** them —
promoting the valuable, pruning the stale, stamping what a human vouches for —
whenever a human reviews.

**Everything below is the *why*.**

## Contents

- [The premise: output is bounded by context](#the-premise-output-is-bounded-by-context)
- [Why code is no longer enough](#why-code-is-no-longer-enough)
- [Keeping the wheel](#keeping-the-wheel)
- [Where it sits](#where-it-sits)
- [Old tree, new shoots](#old-tree-new-shoots)
- [What goes in](#what-goes-in)
- [The mechanism: the provenance stamp](#the-mechanism-the-provenance-stamp)
- [Lifecycle: accumulate → distill](#lifecycle-accumulate--distill)
- [Writing conventions](#writing-conventions)

---

## The premise: output is bounded by context

An LLM's output is a function of its context. Give it the context that decides the
answer and the result moves toward what the project wants; starve it and it fills
the gap with confident guesses — which is where wrong-but-plausible work comes from.

The asymmetry is the point. More context has trade-offs (noise, diluted attention,
tokens); *missing the context that decides the answer* has none — it just loses. A
capable model reasoning without the deciding information still produces wrong work;
its ceiling is set by what it can see.

This is why PCR has two halves: **accumulate** the judgment that would otherwise
evaporate (too little is reliably bad), and **distill** it — pruning noise, keeping
the current truth fresh (too much or stale is bad too).

---

## Why code is no longer enough

Code records the **result state**: what the system finally looks like. It
structurally drops three things a collaborator needs:

1. **The rejected paths.** The code shows "we chose A," never "we considered B
   and C; B was killed because X." So the next collaborator sees A, asks "why
   not B?", tries B, and walks into the same wall.
2. **The status of a choice.** Is this a deliberate, closed decision, or a
   stopgap awaiting review? The code looks identical either way, but the two
   call for opposite actions.
3. **The provenance of a judgment.** On what constraints, trade-offs, and whose
   call did this rest? When the constraints change, the decision may need
   reopening — but only if you recorded what it was hanging on.

In the pre-AI era these lived in maintainers' heads and travelled by
**continuity**: code review, mentorship, "ask the person who wrote it." Teams
were continuous; the knowledge was tacit but unbroken.

An AI collaborator has **no continuity**. Every session is an amnesiac, capable,
and *self-directed* newcomer. It does not "ask the person who wrote it" — it
reasons, doubts, and acts on its own. Tacit knowledge is, to it, nonexistent. So
the judgment layer that always existed but hid in human heads must now be made
into an **explicit artifact** — or it re-evaporates, once per session, forever.

PCR is that artifact. What it preserves is not *what the code is*, but *how the
judgment was reached* — so that thinking already paid for is not paid for again.

---

## Keeping the wheel

AI can iterate faster than any human can review. That forces a dilemma: review
every step and you become the bottleneck, erasing the speed; review nothing and
the work quietly drifts from what you wanted.

PCR is a way out. A human sets direction at a few durable points — the records
they vouch for — and the AI runs fast within those rails. Control moves from
reviewing every action, which doesn't scale, to owning the direction, which does.
The vouched stamp is the steering input: a vouched call isn't re-opened each
session without a real reason, so a decision you make once keeps shaping the work,
session after session, instead of being re-argued every time.

So PCR is also a **harness**: a way to hand the AI execution speed while a human
keeps the wheel. The scarce human act often shifts from doing the work, or checking
it line by line, to setting and maintaining the direction the records encode.

---

## Where it sits

```
Guiding philosophy   Context Engineering   — curate what's in the model's context
        └ Methodology   Project Context Records   — persist the project's slice of it
                └ Mechanism   the provenance stamp   — mark who stands behind a claim
```

---

## Old tree, new shoots

PCR is the AI-era descendant of **Architecture Decision Records (ADR)** — a
convention introduced by Michael Nygard in 2011 and since grown into an
[ecosystem of tooling and templates][adr-hub]. An ADR records each significant
decision as a small, numbered, version-controlled file stating its *context*,
the *decision*, and its *consequences*; a decided record is never edited — to
change it, you write a new one that **supersedes** it, leaving an append-only
trail.

PCR keeps ADR's best instinct — *knowledge lives in the repo, reviewed and
versioned with the code, not in a wiki* — and grafts on three shoots for the new
reader:

1. **Decisions → context.** ADR centers one significant decision per file, with
   its context and consequences. PCR widens the unit to the whole meta-layer:
   decisions *and* architecture, mental models, deliberate divergences, gotchas,
   and in-flight plans. A decision is one slice of a project's context, not all of it.
2. **Immutable-and-stacked → single-and-fresh.** ADR preserves history by
   freezing each decided file and appending a new one that supersedes it; the
   current truth ends up scattered across that supersede chain. PCR keeps the
   **current conclusion in one fresh place** and lets **git** hold the evolution.
   An amnesiac agent re-reading a supersede chain to find today's answer is pure
   waste; give it one trustworthy answer and send history to the log. Rationale
   that still bears on the decision stays in the current entry; only the incidental
   evolution goes to git.
3. **Reader = human → reader = self-directed amnesiac agent.** ADR only
   describes, because a human reads the consequences and self-regulates. An agent
   will "discover" a settled thing and act on it. So a PCR entry may carry an
   **action directive to the agent** ("this is out of contract; don't re-flag
   it"), not just a description.

---

## What goes in

The **meta-layer** of a project: why it is shaped this way, the architecture,
maintainer decisions, intent, deliberate divergences, mental models, hard-won
gotchas, and plans currently in flight.

Negative definition, often sharper: **anything true about the project that the code
can't tell you, and that stays useful beyond the moment.**

Capture is **broad** — record anything plausibly useful, cheaply, as you go,
ephemeral plans and in-flight reasoning included. Value is judged later, at
**distillation** (below), not at capture time: what survives is the residue still
useful beyond the moment.

---

## The mechanism: the provenance stamp

This is the one piece of hard currency, and it rests on a first principle:

> In the AI era, text is cheap and **AI-authored by default**. The scarce,
> valuable act is a **human putting their seal on a claim.**

So the rule is a single bit:

- **No stamp = AI-accumulated.** The default substrate. Treat it as
  challengeable — question it, and verify it freely.
- **`[VOUCHED @handle]` = a human vouched for it.** Treat it as foundation: don't
  re-verify or reopen it for its own sake — do either only on new evidence, a
  changed constraint, or a human's say-so. A stamp marks a single line (at the end
  of it) or a whole file (at the top), and represents explicit human vouching: typed
  by a human, or added by an agent only on a human's explicit instruction. A human
  reading past a claim, or not objecting, never counts.

```
Timestamps are stored as UTC, converted only at the edges — settled after a DST bug.   [VOUCHED @hyf0]

Raising the cache TTL to 1h is probably safe.   ← no stamp: AI-accumulated, verify freely
```

**The human seal is optional — for continuity, not for control.** The
agent-accumulated substrate already carries the memory: an agent inherits what was
recorded, vouched or not. What the seal adds is the harness from [Keeping the
wheel](#keeping-the-wheel) — the human direction that holds across sessions. So
vouch where the stakes justify it, and leave the rest as the honest default.

**Why a stamp, and only one kind.** The worst way an AI-maintained knowledge base
fails is that the AI's own guesses get taken for facts a human has confirmed — a
later agent treats a machine-made assumption as settled and builds on it. The stamp
draws exactly that line, and only that line: **vouched for by a human, or not.**
Finer distinctions — *decision or observation? settled or still tentative?* —
belong in the entry's own text, not in more kinds of stamp. Start with this one;
add more only if real use proves you need it.

---

## Lifecycle: accumulate → distill

- **Accumulate** (cheap, default, by agents): record context proactively while
  working — and whenever a human asks — and keep existing records fresh as your
  changes touch them. Volume is fine; noise is expected.
- **Distill** (scarce, by humans): a review pass that **promotes** the valuable,
  **prunes** what's wrong or obsolete, and **vouches** for what holds — the part
  agents can't do for themselves. This is the human seal applied as a recurring
  practice, and where "implementation plans tracked temporarily" become "the
  valuable thing that remains."

---

## Writing conventions

- **One topic per file.** Cross-link related entries with standard relative
  Markdown links (`[other-topic](./other-topic.md)`) — clickable on GitHub,
  unambiguous, and tool-agnostic.
- **Keep the current truth fresh.** Drift is the death risk: a confident record
  that no longer matches reality flips from asset to **trap** — an agent will act
  on it with full confidence. A stale record is worse than no record. When your
  change affects an entry, update the entry in the same change.
- **Capture the why**, not just the what: the trade-off, the alternatives
  rejected, the known pitfalls. Lead with the principle or intuition.
- **Write so a collaborator gets it without reading the code internals.** The
  entry stands on its own as prose; an agent reads it and *gets it*.
- **No fixed format — on purpose.** A record is just prose that conveys the why.
  A stricter shape may emerge from real use; don't impose one up front.

---

[adr-hub]: https://adr.github.io/
