# Freshness: the temporal side of provenance

The [provenance stamp](./one-bit-stamp.md) answers *who* — human-vouched or AI-accumulated. It does not answer whether the words still match the project. A vouch that has outlived the direction or code it covers is the stale-record trap with human approval still attached: settled-looking, and wrong.

## The decision

Freshness comes from several small signals working together; no date can detect it alone.

1. **The vouch carries a date** — `[VOUCHED @hyf0 2026-07-08]`. It is metadata on the existing bit, not a new kind of stamp: it records when the human last accepted the direction. Legacy undated stamps remain valid, but gain a date only when a human re-vouches; an agent never guesses one from git history.
2. **Routes expose scope** — a [map](./the-map.md) names the code area or hotspot and links the exact record or heading. Code breadcrumbs fire at the narrowest relevant spot. Neither needs a required schema, but both give a reviewer something concrete to compare with the diff.
3. **Normal changes update the stale side** — when code and a record disagree, the code is not automatically right. Decide whether implementation drifted from intended direction or description drifted from reality, then update the stale side. A vouched conflict goes back to a human.
4. **Evidence survives with the claim** — tests, reproducible commands, committed artifacts, stable URLs, and commit hashes can be checked later. Temporary paths, missing screenshots, and one-off session output cannot support a durable audit unless the artifact is preserved.
5. **Distillation rechecks the set** — the [distillation draft](./distill-draft.md) re-reads all records against the areas and evidence they describe, using map routes where present, then flags plausible aging instead of claiming mechanical certainty.

## Why the date doesn't violate the one-bit rule

[one-bit-stamp](./one-bit-stamp.md) rejects a *richer status scheme* — more epistemic states. The date is none of that: it adds no new answer to "what kind of claim is this"; it timestamps the one bit that is already there. The approval line stays exactly one bit wide, while scope and evidence do separate jobs.
