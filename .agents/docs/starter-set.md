# The starter set: why PCR names first records

PCR deliberately fixes no format and no list of what qualifies. But adopters kept needing the same first records — the pattern that prompted this record was a maintainer telling agents, project after project, to create the same technology-stack file by hand. A methodology that leaves the first move to be re-invented per project is under-specified in the one place every adopter passes through.

## The decision

[The README names a small starter set](../../README.md#the-starter-set) — goal, technology-stack, architecture, conventions, gotchas, plus `DESIGN.md` (the google-labs-code visual-identity spec, at the repo root, enrolled via the map) when the project has a visual surface — and `pcr-setup` offers to draft the applicable ones from the codebase at adoption. The README section is the normative list; this record holds why naming one doesn't break PCR's own rules.

## Why this doesn't break "no fixed list"

The no-fixed-list rule guards against inventing structure ahead of need ("a stricter shape may emerge from real use; don't impose one up front"). The starter set is that rule working, not an exception to it: each topic is on the list because real use kept asking for it, and the list grows only the same way. What stays unfixed is everything the rule actually protects — format, completeness, and what else a project records.

## Why the adoption block names them too

`pcr-setup` seeds the starter set once, at adoption — but the skill is optional (the hand-paste path never runs it), and a missing record is an *absence*, which none of the "record as you go" triggers fire on: they are all events. The adoption block is the only channel guaranteed to reach every session of every adopted project, so it carries a dedicated "The basics" bullet listing them — a hand-pasted adoption still learns them, an agent in a thin folder notices the gap, and the list form is scannable where a prose clause washes out. The bullet is self-limiting — "draft the missing ones that apply" — so it goes quiet once the records exist. It sits **last** in the block, deliberately: it is the one part expected to grow (a topic joins when real use keeps asking), and growth at the tail never displaces the stable behavioral rules above it. It is the block's second bootstrap trigger, alongside "distill a map": both are knowing exceptions to the every-session bar, carried because no other channel exists.

## The cold start it fixes

An empty records folder is where adoption is most likely to stall: nothing returns value until someone writes, and nobody knows what to write first. Seeding turns day one into a reviewed skeleton — drafted by the agent from the repo's own evidence, corrected and vouched by a human, inherited by the next session.

Related: [the-map](./the-map.md) (the other end of the folder's growth), [conventions-not-tooling](./conventions-not-tooling.md).
