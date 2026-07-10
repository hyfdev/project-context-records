# Distillation: agent drafts, human approves

Distillation — prune the wrong, promote the valuable, and vouch the direction that should keep holding — is the human half of PCR, and also the half most likely not to happen: it costs the exact thing PCR exists to conserve, a maintainer's scarce attention. Left as a from-scratch authoring task, the valve rusts shut and the records grow into an unpruned pile.

## The decision

The agent drafts the distillation; the human approves it. A pass produces a reviewable diff over the records, sorted into the moves a human is slow to find by hand:

- **contradicted** — records that no longer match the code or durable evidence they describe, after deciding which side drifted;
- **redundant** — near-duplicate records that should merge;
- **buried** — valuable context sitting in an accumulated pile, worth promoting;
- **map drift** — records or important headings missing from the map, stale code-area routes, or links pointing at content that moved;
- **load-bearing but unvouched** — unstamped direction that other records or code lean on, surfaced for a human to vouch or reject;
- **unsupported facts** — factual claims whose test, command, artifact, URL, or commit evidence is missing or no longer supports them;
- **aging vouches** — vouched text plausibly affected by changes to the code areas, hotspots, constraints, or evidence it covers. The stamp date is a review clue, not proof of staleness.

The human approves and edits the draft, then vouches only the direction they explicitly accept. Facts remain supported by durable evidence rather than approval.

## Why this stays consistent with the rest of PCR

It is the same harness PCR already applies to code, turned on the records. PCR's bet is that a human owns the direction and a self-directed agent does the labor within it. Distillation was the one place the bet wasn't cashed — the human was still doing the labor. Drafting moves it: the agent does the finding, the human keeps the deciding. Nothing about *who vouches* changes: an agent-drafted "vouch this direction" is a proposal, never a stamp, and factual verification never flips the approval bit.

Related: [the-map](./the-map.md), [freshness](./freshness.md), [unattended-runs](./unattended-runs.md) (the no-human case: the loop tidies its own unstamped layer).
