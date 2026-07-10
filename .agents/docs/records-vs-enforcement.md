# Records and enforcement: put each constraint in the strongest durable form

PCR exists to preserve project judgment, not to turn every useful fact or rule into prose. A prose record can explain a constraint, but it cannot enforce one; using it as the only home for a machine-checkable invariant leaves correctness dependent on retrieval and instruction-following.

## The decision

Use the strongest durable form that fits the information:

- Put machine-checkable constraints in types, tests, lints, CI gates, or the implementation structure itself. A PCR record may explain why the constraint exists and when it should be reconsidered, but it is not the enforcement mechanism.
- Put rationale that matters at one code hotspot beside that code. Link to a record when the full reasoning is too large or cross-cutting.
- Put temporary execution state in an issue or one replaceable live plan. Preserve only the judgment that survives the work.
- Put cross-cutting maintainer decisions, intent, rejected alternatives, mental models, and other context that must remain prose in PCR.

This is not a hierarchy of importance. It is a choice of representation: a test is better at detecting a broken invariant; a nearby comment is more likely to be seen when that code is edited; a record is better at preserving reasoning that spans code areas and sessions. Important context can use more than one form without duplicating the same content: the executable artifact enforces the rule, the local link routes the reader, and the record explains the judgment.

## Consequences

"Not visible in the code" is no longer enough on its own to earn a record. First ask whether a stronger durable artifact can carry the information. Records stay smaller, factual claims retain reproducible evidence, and an agent that misses a record is less likely to violate an invariant the repository could have checked directly.

This decision does not add tooling to PCR. Projects choose their own types, tests, lints, CI, and code comments; PCR only states where prose stops being the best representation.

Related: [existing docs](./existing-docs.md), [retrieval map](./the-map.md), [freshness](./freshness.md), [conventions, not tooling](./conventions-not-tooling.md).
