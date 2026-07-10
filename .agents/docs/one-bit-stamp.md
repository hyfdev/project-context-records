# Why the stamp is one bit (human-vouched, or not)

A record's approval provenance is a single bit: **a human explicitly accepted the covered words as project direction, or the text is AI-accumulated.** That's the whole stamp. Everything finer goes in prose or factual evidence.

## The decision

The provenance stamp `[VOUCHED @handle YYYY-MM-DD]` marks one distinction and only one: explicitly accepted by the named human vs not. It is approval for project direction, not proof that an empirical claim is true. We deliberately did not build richer states.

## What we rejected

An earlier design had a four-way epistemic status — `observed` (ran it), `inferred` (reasoned, unverified), `decided` (a judgment call), `open` (unsettled) — plus sub-flags like `settled` vs `provisional`. It is expressive, but it is four stamps doing the job one bit already does.

## Why one bit is the one that matters

The deepest failure of an AI-maintained knowledge base is the AI's own proposal getting taken for direction a human accepted — a later agent builds on a machine assumption as if it were settled. The single explicit-approval bit fixes exactly that. It does not say whether a statement is a decision or observation, settled or tentative, or well-supported or weak; those distinctions belong in the entry's text, and factual support belongs in durable evidence.

## The rule that keeps it honest

Because the bit is load-bearing, it counts only when the named human **explicitly** vouches. A human reading past text, approving unrelated changes, or not objecting is never a stamp. (This is also why this very file is unstamped until a human says otherwise.)

The text marker is not an authenticated signature: anyone can type it. When reviewing a change, treat a newly added stamp as an untrusted claim unless the named human explicitly confirms it; a stamp already present on the target branch is inherited project state. Repositories that need stronger authorization can protect record paths with their normal review controls, without changing PCR's format.

A stamp declares one exact scope: at a non-heading line's end it covers that line; as the first nonblank line below a non-title heading it covers that section until the next heading of the same or higher level; as the first nonblank line below the document title it covers the whole file. Do not put any new stamp in heading text: GitHub derives the heading's link anchor from that text, so stamping or re-vouching it would break exact-heading routes in the map.

Legacy placement remains valid. A standalone stamp before the document title still covers the whole file. A stamp already inside a heading keeps any scope the project previously declared; when that scope is undocumented, preserve the pre-update interpretation and surface the ambiguity when work depends on it. Never move or reinterpret either form until the named human re-vouches or explicitly approves the migration.

Editing is held to the same bar as stamping: materially changing covered words drops the stamp until a human re-vouches — otherwise an agent's new words launder themselves under old approval. Changing a heading level, inserting or removing a boundary heading, moving a stamp, or rewrapping a stamped line is also material whenever it changes the set of covered words. A formatting-only change keeps the stamp only when that covered set is identical.

## The one exception that isn't one: a date

A vouch carries the date it was made — `[VOUCHED @handle 2026-07-08]`. That is a timestamp on the same bit, not a second bit: the status distinctions this file rejects stay barred from the stamp. Legacy undated stamps remain vouched, but an agent never invents or backfills a date; the human adds one when re-vouching. Why the temporal dimension exists, and what it cannot detect alone, is [freshness](./freshness.md)'s topic.

The naming of the methodology this mechanism sits inside is recorded in [naming](./naming.md).
