# Updating requires a fresh skill and a marked block

PCR ships as a paste-in block plus a setup skill, not as software with a version manager — so "how do adopted projects get updates?" needs an answer that stays light and honest about where the latest text comes from. An installed skill contains a snapshot of the block; re-running that snapshot cannot discover a newer one by itself. The operative procedure lives in [the skill](../../skills/pcr-setup/SKILL.md); this record holds why it works the way it does.

## The decision

Updating has two explicit steps: refresh the installed skill with `npx skills update pcr-setup -g`, then run `/pcr-setup` in the project. The first step obtains the latest canonical block; the second applies it.

The canonical block is bounded by `<!-- PCR:START -->` and `<!-- PCR:END -->`. An update replaces only that marked region and carries over the records-folder path. A safe update first requires exactly one start marker followed by exactly one end marker, with no other tool's marker line inside the region; if a marker is missing, duplicated, or reversed, or another tool's marker sits inside the region, setup stops and reports the ambiguity instead of guessing at ownership. The methodology owns the marked text; project-specific routing, commands, and policies live outside it. Records are never touched, and seeding never re-runs on a folder that already has records.

A legacy unmarked block gets one careful migration. Setup classifies the old text before editing, moves clearly local additions outside the new PCR markers and every other generated or third-party marker region without changing their wording, then replaces the prior methodology text. If a clause mixes old methodology and a possible local edit, setup stops and shows the proposed split for human confirmation. An update must never guess away a project rule merely because an older block had no ownership boundary.

## Why marked replacement, not merge

Merging arbitrary local edits with upstream changes would need three-way diffing and conflict handling — tooling, which [stays outside the spec](./conventions-not-tooling.md). Two plain HTML comments create the ownership boundary without requiring a parser or CI: canonical text wins inside; project text survives outside. Every marked project can run the same current block without turning a safe update into a destructive rewrite.

Related: [starter-set](./starter-set.md).
