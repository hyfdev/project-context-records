# Contributing

PCR grows by one rule: **every addition must be paid for by recurring, real-use pain.** A proposal that starts from "it would be nice if" is parked; one that starts from "this failed on me, twice, in real projects" gets taken seriously. The bar applies to the maintainers too.

Ways to contribute, in order of value:

- **Report an observed failure.** An agent read the adoption block and still skipped a rule — didn't check the map, re-litigated a vouched decision, wrote a manifest dump into `technology-stack.md`. Open an issue describing what the agent did and what the block said. The block is maintained like a versioned prompt: observed compliance failures are exactly the tuning data it evolves on.
- **Report a recurring need.** You keep hand-writing the same kind of record across projects, or keep hitting a situation the methodology is silent on. Name the pain and show it recurred; the lightest form that covers it gets considered.
- **Propose a change.** Read [`.agents/docs/`](./.agents/docs/) first — the records hold what was already decided and why, including the rejected alternatives; re-proposing a recorded rejection needs new evidence, the same bar a vouched line sets. Anything that would require software to adopt is out of scope for the spec ([conventions, not tooling](./.agents/docs/conventions-not-tooling.md)) — build it as a separate tool that reads PCR records instead. And mind the audience split: an adopted project's agents read **only the block** — they never fetch this repo — so agent-facing behavior goes in the block or it effectively doesn't exist; the README is for humans (the why, and the human-side practices).

Working in this repo, `AGENTS.md` is the source of truth for conventions: the canonical block copies, the translation rule, soft-wrap.
