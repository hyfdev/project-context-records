# Unattended runs: the unstamped layer is the loop's to keep

The methodology's author's own dominant usage is loop engineering: adopt PCR in a project, then run agents in iterations — no human between them — until the thing is built. That pattern exposed a gap: distillation was human-gated, so an unattended run accumulates forever and the valve never opens — two hundred iterations leave a landfill nobody prunes, and later iterations drown in earlier ones' stale notes.

## The decision

Distillation splits along the stamp. The **unstamped layer** — the loop's own working memory — the loop maintains itself: merge duplicates, prune dead in-flight notes, keep the map honest, keep one live plan record fresh (single-and-fresh applied to loop state). The **vouched layer**, and the act of vouching, stay human-only exactly as before; unattended, the loop queues what needs a human — proposed vouches, conflicts between reality and a vouched call — and its exit act is the distillation draft. The agent-facing rules live in the block's **Unattended** bullet — an adopted agent never reads this repo, so a rule outside the block does not exist for it; [the README's "Unattended runs"](../../README.md#unattended-runs) is the why, for the human setting the loop up.

## The three acts

**Before the loop, the human steers by vouching.** Direction that must survive a hundred iterations is written and vouched before the first one: the goal record, the architecture bets as `architecture.md` (born as a bet, maturing into description), hard constraints in the instructions file outside the block where they fire every session. On a greenfield repo this direction *is* the seed; `pcr-setup` drafts it from the human's brief. The boundary cuts both ways: vouched records are rails the loop may not re-litigate, and what stays unstamped is explicitly delegated — the loop's to decide and revise. If the loop finds evidence against a vouched call, it records the conflict and stays inside the rails unless they make progress impossible; silence is the one thing it may not choose.

**During the loop, the records are its only memory.** Iteration N+1 inherits iteration N's judgment through the records or not at all. The current plan stays one live record, overwritten in place as truth changes — single-and-fresh applied to loop state; git keeps the trail.

**After the loop, the records are the audit trail.** The exit distillation says what was decided, what to vouch, what to prune, and where reality argued with a vouched call — a diff of judgment instead of two hundred transcripts; the next run starts on distilled, partly-vouched ground.

## What we rejected

- **No self-distillation at all** (the prior state) — the one-bit logic never required a human to tidy AI notes. The human gate exists so AI guesses can't impersonate human confirmation; pruning your own unstamped text impersonates nothing, and the alternative is unbounded noise.
- **Letting sustained verification vouch** — "fifty green runs, surely that counts." No: verification is evidence about a claim; the stamp is a human taking responsibility for it. Evidence strengthens the prose ("verified across N runs" is worth writing down); it never flips the bit. An unattended run ends with zero new vouches by construction.
- **Run supervision** — a finish-line rule ("done is what the vouched goal record says, not what feels finished") and mid-run observability guidance were drafted and cut: judging termination and monitoring progress are the loop harness's job, not the methodology's. PCR keeps the memory and its authority; the harness keeps the run.
- **Three new rail files** (`goal.md` + `non-goals.md` + `constraints.md`) — partially cut, after two over-corrections. `constraints.md` is a real conflict: hard rules belong in the instructions file's push layer, tech constraints in `technology-stack.md`. `non-goals.md` folds into the goal record — one topic. But the goal itself earned a place in the basics: intent is meta-layer with no other home — the README pitches to users, the goal record speaks to collaborators — and a methodology whose own tagline names "the intent" had no file for it. Where a README already states it all, enrollment covers it.

Related: [one-bit-stamp](./one-bit-stamp.md), [distill-draft](./distill-draft.md), [freshness](./freshness.md).
