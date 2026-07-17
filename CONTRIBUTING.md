# Contributing

PCR grows by one rule: **every addition must be paid for by recurring, real-use pain.** A proposal that starts from "it would be nice if" is parked; one that starts from "this failed on me, twice, in real projects" gets taken seriously. The bar applies to the maintainers too.

The growth path is **promotion**. A pattern that keeps recurring in real adopted projects gets promoted into the methodology — as a suggested topic, or as an opt-in pattern carrying an applicability condition and the minimum format that use proved necessary. That is how the current pieces earned their place: the decision ledger began as one project's `DESIGN-decisions.md`, and its format constraints exist because the free-form original drifted. A promotion proposal shows the recurrence; the methodology supplies the lightest form that covers it.

Ways to contribute, in order of value:

- **Report an observed failure.** An agent read the adoption block and still skipped a rule — didn't check the map, re-litigated a vouched decision, edited its own `loop-goal.md`, wrote a manifest dump into `technology-stack.md`. Report the task, agent/tool/model, the block version (commit), the relevant records, what the agent did and what it should have done, and a reproducible project state when one can be shared. The block is maintained like a versioned prompt: observed compliance failures are exactly the tuning data it evolves on.
- **Report a recurring need.** You keep hand-writing the same kind of record across projects, or keep hitting a situation the methodology is silent on. Name the pain and show it recurred; the lightest form that covers it gets considered.
- **Propose a change.** Mind the audience split: an adopted project's agents read **only the block** — they never fetch this repo — so agent-facing behavior goes in the block or it effectively doesn't exist; the README is for humans. And nothing in the spec may require software to adopt: anything that needs a tool is built as a separate project that reads records, never as a requirement of the convention.

## Evaluating an agent-facing change

Treat the adoption block as a prompt whose success is behavior, not prose quality. When a change claims to improve compliance, keep at least one real task that previously failed and compare the current block with the candidate under the same project state, task, agent/model, and budget. Record whether the agent opened the relevant record before acting, violated a known decision, loaded irrelevant context, needed reviewer correction, or followed stale context without surfacing a conflict. Include an unrelated task when the new rule might add noise. A small reproducible case is worth more than a broad claim.

For work in this repo, `AGENTS.md` holds the conventions: the canonical block copies, the translation rule, soft-wrap.
