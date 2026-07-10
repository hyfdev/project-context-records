# Contributing

PCR grows by one rule: **every addition must be paid for by recurring, real-use pain.** A proposal that starts from "it would be nice if" is parked; one that starts from "this failed on me, twice, in real projects" gets taken seriously. The bar applies to the maintainers too.

Ways to contribute, in order of value:

- **Report an observed failure.** An agent read the adoption block and still skipped a rule — didn't check the map, re-litigated a vouched decision, wrote a manifest dump into `technology-stack.md`. Report the task, agent/tool/model, exact block or methodology commit, relevant records, whether the agent opened them before acting, expected behavior, actual behavior, and a reproducible project state when one can be shared. The block is maintained like a versioned prompt: observed compliance failures are exactly the tuning data it evolves on.
- **Report a recurring need.** You keep hand-writing the same kind of record across projects, or keep hitting a situation the methodology is silent on. Name the pain and show it recurred; the lightest form that covers it gets considered.
- **Propose a change.** Read [`.agents/docs/`](./.agents/docs/) first — the records hold what was already decided and why, including rejected alternatives. A vouched rejection needs new evidence, a changed constraint, or the named human's say-so before it is reopened; an unstamped rejection is challengeable, but address its recorded rationale rather than ignoring it. Anything that would require software to adopt is out of scope for the spec ([conventions, not tooling](./.agents/docs/conventions-not-tooling.md)) — build it as a separate tool that reads PCR records instead. And mind the audience split: an adopted project's agents read **only the block** — they never fetch this repo — so agent-facing behavior goes in the block or it effectively doesn't exist; the README is for humans (the why, and the human-side practices).

## Evaluating an agent-facing change

Treat the adoption block as a prompt whose success is behavior, not prose quality. When a change claims to improve compliance, keep at least one real task that previously failed and compare the current block with the candidate under the same project state, task, agent/model, and budget. Record whether the agent opened the exact relevant record before acting, violated a known decision, loaded irrelevant context, needed reviewer correction, or followed stale context without surfacing a conflict. Include an unrelated task when the new rule might add noise. A small reproducible case is more valuable than a broad claim; universal score thresholds can wait for a larger case set.

Working in this repo, `AGENTS.md` is the source of truth for conventions: the canonical block copies, the translation rule, soft-wrap.
