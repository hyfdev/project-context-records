# Conventions, not tooling: PCR stays light by decision

PCR could grow two ways: into a verification suite — records compiled into checks, CI enforcing vouched invariants, bots drafting distillation — or stay what it is: prose conventions adoptable by pasting one block. The fork was weighed deliberately (July 2026) and the light side chosen. Anyone proposing to add a mechanism to the spec should read this first.

## The decision

The spec is prose conventions only. Nothing in PCR may require software to adopt: no PCR-specific CI, bots, parsers, front matter, or record schema. Adoption remains plain Markdown plus two HTML comments that bound safe updates; a project that pastes the block manually needs no program. Growth happens in content — what to record, how to write it, what to seed — not in PCR machinery.

## Why light won

- **Standards win by being trivially adoptable.** ADR itself, Conventional Commits, semver: prose conventions that spread because adoption cost nothing and no tool had to agree. The paste-in block *is* the product; every mechanism added to the spec taxes it.
- **The middle is the worst position.** Half-mechanisms — a required index format, a PCR lint, a bot — spend the ten-second adoption without buying real enforcement. PCR enforcement is either whole (a suite) or absent (conventions); partial enforcement pays both costs and collects neither benefit. Projects still put machine-checkable invariants in their normal types, tests, lints, and CI ([records and enforcement](./records-vs-enforcement.md)).
- **A verification suite is a different project.** Per-language checkers, CI integrations, a maintenance surface — a different lifecycle from a methodology document. It can exist later as a separate tool that *consumes* PCR records, the way adr-tools consumes ADR, without the convention ever depending on it.

## What this rules out — and what it doesn't

Out of the spec: anything an adopter must install or run. Not ruled out: a project's existing checks or optional third-party tools that read records and inspect routes — they stay outside the spec. The [distill draft](./distill-draft.md) stays in because it is a practice an agent performs from prose instructions, not a required tool; the [map](./the-map.md) stays in because it is a Markdown file, not a format anything must parse.
