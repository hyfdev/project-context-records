# Naming: why "Project Context Records", not "Agent Context Records"

[VOUCHED @hyf0]

The records are the **project's** shared memory, not any one agent's. "Project" says that; "Agent" would have said the wrong thing.

## The decision

The methodology is named **Project Context Records (PCR)**. Middle word **Context** (broad — any durable context, not just decisions); first word **Project**, not **Agent**.

## Why not "Agent Context Records"

`Agent` was the leading alternative — it signals the AI era and "records an agent accumulates". Two reasons it lost:

- **It reads wrong cold.** In 2026, "context" is owned by "the context window". An outsider parses *Agent Context* as "a dump of what was in the agent's context window" — session logs, a memory dump — the opposite of a curated, durable archive. *Project Context* has no such collision: it reads as "the project's background", which is right.
- **The records belong to the project, not the agent.** They are shared memory, versioned with the repo, inherited by every collaborator, human or agent. Naming them after one transient reader misframes what they are.

The AI-era signal that `Agent` would have carried is carried instead by the framing ("for an amnesiac AI collaborator"), not by the title — a better place for it.

## Why not a grander name

Earlier attempts pitched at the wrong altitude. `-Engineering` names (e.g. "Judgment Engineering") sit at the *guiding-philosophy* level and compete with Context Engineering; PCR is a *methodology*, one rung down — a sibling of ADR. The name should sit where ADR sits (`[Subject] Records`), which is what "Project Context Records" does.

Ladder: **Context Engineering** (philosophy) → **Project Context Records** (methodology) → the [provenance stamp](./one-bit-stamp.md) (mechanism).
