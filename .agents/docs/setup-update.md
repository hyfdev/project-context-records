# Re-running setup is the update mechanism

PCR ships as a paste-in block plus a setup skill, not as software with a version manager — so "how do adopted projects get updates?" needs an answer that stays light. The answer: run `/pcr-setup` again. Setup is idempotent; on an adopted project it becomes update. The operative procedure lives in [the skill](../../skills/pcr-setup/SKILL.md); this record holds why it works the way it does.

## The decision

An update replaces the project's PCR block with the canonical one and touches nothing else: the block belongs to the methodology; the records — and the records-folder path the project chose, the one parameter carried over — belong to the project. Seeding never re-runs on a folder that already has records.

## Why canonical-wins, not merge

Merging local block edits with upstream changes would need a version marker, three-way diffing, conflict handling — tooling, which [stays outside the spec](./conventions-not-tooling.md). A hard boundary — the block is the methodology's, everything else is the project's — makes the update a plain text replacement an agent does reliably with file edits, and it keeps the block trustworthy: every adopted project runs the same current block, not a drifted local dialect of it.

Related: [starter-set](./starter-set.md).
