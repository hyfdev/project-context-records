# The starter set: why PCR names first records

PCR deliberately fixes no format and no list of what qualifies. But adopters kept needing the same first records — the pattern that prompted this record was a maintainer telling agents, project after project, to create the same technology-stack file by hand. A methodology that leaves the first move to be re-invented per project is under-specified in the one place every adopter passes through.

## The decision

The block's **The basics** bullet fixes the list — goal, technology-stack, architecture, conventions, gotchas, plus `DESIGN.md` when the project has a visual surface — and `pcr-setup` offers to draft the applicable ones at adoption. The README introduces the set; this record holds the per-topic reasoning, and why naming a list doesn't break PCR's own rules.

## The topics, and what earns each its place

- **goal** — the most upstream judgment: what this is trying to be, for whom, and the non-goals that keep scope honest. Its home is a record, not the README — the README pitches to users; the goal record speaks to collaborators and holds what users don't need: the refusals, the priorities, the why. A README that already states it all is enrolled, not twinned.
- **technology-stack** — the whys the manifest can't say: why these tools over the defaults they displaced, what must not be introduced, what is pinned and why. The record keeps the why; the one-line rules it justifies ("use pnpm", "never add X") are every-session material and belong in the instructions file, which links here.
- **architecture** — the shape as the maintainers hold it: the units, the boundaries between them, and why the lines are where they are. On a greenfield repo it is born as the bets and matures into description as code appears.
- **conventions** — deliberate departures from ecosystem defaults, so a departure reads as a decision, not an accident a helpful newcomer should fix.
- **gotchas** — traps already paid for: things that look safe and aren't, each with its why.
- **`DESIGN.md`** — only for a project with a visual surface: the visual identity described to coding agents — machine-readable design tokens (colors, typography, spacing, components) in front matter, plus the prose why — per the [design.md spec](https://github.com/google-labs-code/design.md). By that convention it lives at the repo root and is enrolled via the map; its ecosystem ships a linter (`npx @google/design.md lint DESIGN.md` — token references, WCAG contrast, schema keys), and where the file exists it stays lint-clean.

## Why this doesn't break "no fixed list"

The no-fixed-list rule guards against inventing structure ahead of need ("a stricter shape may emerge from real use; don't impose one up front"). The starter set is that rule working, not an exception to it: each topic is on the list because real use kept asking for it, and the list grows only the same way. What stays unfixed is everything the rule actually protects — format, completeness, and what else a project records.

## Why the adoption block names them too

`pcr-setup` seeds the starter set once, at adoption — but the skill is optional (the hand-paste path never runs it), and a missing record is an *absence*, which none of the "record as you go" triggers fire on: they are all events. The adoption block is the only channel guaranteed to reach every session of every adopted project, so it carries a dedicated "The basics" bullet listing them — a hand-pasted adoption still learns them, an agent in a thin folder notices the gap, and the list form is scannable where a prose clause washes out. The bullet is self-limiting — "draft the missing ones that apply" — so it goes quiet once the records exist. It sits **last** in the block, deliberately: it is the one part expected to grow (a topic joins when real use keeps asking), and growth at the tail never displaces the stable behavioral rules above it. It is the block's second bootstrap trigger, alongside "distill a map": both are knowing exceptions to the every-session bar, carried because no other channel exists.

## The cold start it fixes

An empty records folder is where adoption is most likely to stall: nothing returns value until someone writes, and nobody knows what to write first. Seeding turns day one into a reviewed skeleton — drafted by the agent from the repo's own evidence, corrected and vouched by a human, inherited by the next session.

Related: [the-map](./the-map.md) (the other end of the folder's growth), [conventions-not-tooling](./conventions-not-tooling.md).
