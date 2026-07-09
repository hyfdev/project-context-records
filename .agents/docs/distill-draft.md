# Distillation: agent drafts, human approves

Distillation — prune the wrong, promote the valuable, vouch what holds — is the human half of PCR, and also the half most likely not to happen: it costs the exact thing PCR exists to conserve, a maintainer's scarce attention. Left as a from-scratch authoring task, the valve rusts shut and the records grow into an unpruned pile.

## The decision

The agent drafts the distillation; the human approves it. A pass produces a reviewable diff over the records, sorted into the moves a human is slow to find by hand:

- **contradicted** — records that no longer match the code they describe (found by re-reading each against its code);
- **redundant** — near-duplicate records that should merge;
- **buried** — valuable context sitting in an accumulated pile, worth promoting;
- **map drift** — records missing from the map, or map lines pointing at records that moved;
- **load-bearing but unvouched** — unstamped claims that other records or code lean on, surfaced for a human to vouch or reject;
- **aging vouches** — vouched records whose code has changed since the stamp's date.

The human approves, edits, and vouches in one pass.

## Why this stays consistent with the rest of PCR

It is the same harness PCR already applies to code, turned on the records. PCR's bet is that a human owns the direction and a self-directed agent does the labor within it. Distillation was the one place the bet wasn't cashed — the human was still doing the labor. Drafting moves it: the agent does the finding, the human keeps the deciding. Nothing about *who vouches* changes: an agent-drafted "vouch this" is a proposal, never a stamp.

Related: [the-map](./the-map.md), [freshness](./freshness.md), [unattended-runs](./unattended-runs.md) (the no-human case: the loop tidies its own unstamped layer).
