# Freshness: the temporal side of provenance

The [provenance stamp](./one-bit-stamp.md) answers *who* — human-vouched or AI-accumulated. It does not answer *when*, and a vouch that has outlived the code it covers is the stale-record trap with a human seal on it: settled-looking, and wrong. So provenance needs a second, temporal dimension, kept separate from the human/AI one.

## The decision

Two changes, both light.

1. **The vouch carries a date** — `[VOUCHED @hyf0 2026-07-08]`. It is metadata on the existing bit, not a new kind of stamp: it changes nothing about what a vouch *means*, only records when it was made, so "vouched but stale" becomes a state you can see — a year-old `[VOUCHED]` on a module rewritten twice since is the stale-record trap at its worst, settled-looking and wearing a human seal. Agents date every stamp they add: most stamps are typed by an agent on a human's instruction, and the agent knows the date, so it costs nothing. A hand-typed stamp may skip it — git can recover the date later, but the reader shouldn't need archaeology.
2. **Distillation audits freshness** — the [distillation draft](./distill-draft.md) re-reads records against the code they describe and flags vouches whose code has changed since the stamp's date. Detection is a mechanism, not an exhortation: "keep it fresh" stops depending on everyone remembering to.

## Why the date doesn't violate the one-bit rule

[one-bit-stamp](./one-bit-stamp.md) rejects a *richer status scheme* — more epistemic states. The date is none of that: it adds no new answer to "what kind of claim is this"; it timestamps the one bit that is already there. The line the stamp holds — human-vouched or not — stays exactly one bit wide.
