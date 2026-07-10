# The starter set: why PCR names first records

PCR deliberately fixes no format and no list of what qualifies. But adopters kept needing the same first records — the pattern that prompted this record was a maintainer telling agents, project after project, to create the same technology-stack file by hand. A methodology that leaves the first move to be re-invented per project is under-specified in the one place every adopter passes through.

## The decision

The block's **The basics** bullet recommends a starting list — goal, technology-stack, architecture, conventions, gotchas, plus `DESIGN.md` when the project has a visual surface — and `pcr-setup` offers to draft only the applicable gaps at adoption. The README introduces the set; this record holds the per-topic reasoning, and why recommending a list doesn't make it a required schema.

## The topics, and what earns each its place

- **goal** — the most upstream judgment: what this is trying to be, for whom, and the non-goals that keep scope honest. Its home is a record, not the README — the README pitches to users; the goal record speaks to collaborators and holds what users don't need: the refusals, the priorities, the why. A README that already states it all is enrolled, not twinned.
- **technology-stack** — the whys the manifest can't say: why these tools over the defaults they displaced, what is pinned and why. The record keeps the why; every-session commands belong in the instructions file, and machine-checkable restrictions belong in the repository's normal enforcement. Both can link back here.
- **architecture** — the shape as the maintainers hold it: the units, the boundaries between them, and why the lines are where they are. On a greenfield repo it is born as the bets and matures into description as code appears.
- **conventions** — deliberate departures from ecosystem defaults, so a departure reads as a decision, not an accident a helpful newcomer should fix.
- **gotchas** — traps already paid for: things that look safe and aren't, each with its why.
- **`DESIGN.md`** — only for a project with a visual surface: the visual identity described to coding agents — machine-readable design tokens (colors, typography, spacing, components) in front matter, plus the prose why — per the [design.md spec](https://github.com/google-labs-code/design.md). By that convention it lives at the repo root and is enrolled via the map; its ecosystem ships a linter (`npx @google/design.md lint DESIGN.md` — token references, WCAG contrast, schema keys), and where the file exists it stays lint-clean.

## Why this is recommended, not required

The no-fixed-list rule guards against inventing structure ahead of need ("a stricter shape may emerge from real use; don't impose one up front"). Each starter topic is present because real use kept asking for it, but an adopter still skips anything that has no evidence or is already covered by a stronger artifact or enrolled document. What stays unfixed is format, completeness, naming, and what else a project records.

## Why the adoption block names them too

`pcr-setup` offers to seed the applicable starter gaps once, at adoption — but the skill is optional (the hand-paste path never runs it), and a missing record is an *absence*, which none of the "record as you go" triggers fire on: they are all events. The adoption block is the only channel guaranteed to reach every session of every adopted project, so it carries a dedicated "The basics" bullet — a hand-pasted adoption still learns the defaults, an agent in a thin folder notices a relevant gap, and the list form is scannable where a prose clause washes out. The bullet is self-limiting — "draft the missing ones that apply" — so it goes quiet once the applicable context exists. It sits **last** in the block, deliberately: additions at the tail never displace the stable behavioral rules above it. It is the block's second bootstrap trigger, alongside "distill a map": both are knowing exceptions to the every-session bar, carried because no other channel exists.

## The cold start it fixes

An empty records folder is where adoption is most likely to stall: nothing returns value until someone writes, and nobody knows what to write first. Seeding turns day one into a reviewed skeleton — drafted by the agent from the repo's own evidence, corrected and vouched by a human, inherited by the next session.

Related: [the-map](./the-map.md) (the other end of the folder's growth), [conventions-not-tooling](./conventions-not-tooling.md).
