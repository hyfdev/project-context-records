# Why the stamp is one bit (human-vouched, or not)

A record's provenance is a single bit: **a human vouched for it, or it's AI-accumulated.** That's the whole stamp. Everything finer goes in prose.

## The decision

The provenance stamp `[VOUCHED @handle]` marks one distinction and only one: human-vouched vs not. We deliberately did not build richer states.

## What we rejected

An earlier design had a four-way epistemic status — `observed` (ran it), `inferred` (reasoned, unverified), `decided` (a judgment call), `open` (unsettled) — plus sub-flags like `settled` vs `provisional`. It is expressive, but it is four stamps doing the job one bit already does.

## Why one bit is the one that matters

The deepest failure of an AI-maintained knowledge base is the AI's own guesses getting taken for facts a human confirmed — a later agent builds on a machine assumption as if it were settled. The single human/AI bit fixes exactly that, and nothing else fixes it. The finer distinctions (decision vs observation, settled vs tentative) are real, but they belong in the entry's own text, where they cost nothing and confuse no one.

## The rule that keeps it honest

Because the bit is the load-bearing one, the stamp has to be hard to forge: it counts only when a human **explicitly** vouches. A human reading past a line, or not objecting, is never a stamp. (This is also why this very file is unstamped until a human says otherwise.)

A stamp can sit on a single line (at its end) or on a whole file (at the top); the granularity is separate from the bit.

Editing is held to the same bar as stamping: a stamp covers the words it was put on, so materially rewording a vouched line drops the stamp until a human re-vouches — otherwise an agent's new words launder themselves under an old seal. Formatting-only changes keep it.

## The one exception that isn't one: a date

A vouch carries the date it was made — `[VOUCHED @handle 2026-07-08]`. That is a timestamp on the same bit, not a second bit: the status distinctions this file rejects stay barred from the stamp. Why the temporal dimension exists, and how it is audited, is [freshness](./freshness.md)'s topic.

The naming of the methodology this mechanism sits inside is recorded in [naming](./naming.md).
