# Retrieval: why a map file, not co-location or scope-tags

"Read the relevant record" is empty unless something routes an agent from the code in front of it to the record that bears on it — with dozens of records, an agent that no longer reads every file starts to guess.

## The decision

Once the folder outgrows a glance — or the moment [enrolled records](./existing-docs.md) live outside it — retrieval runs through one privileged record: `.agents/docs/README.md`, the map — routing only, content stays in the records. Below that threshold there is deliberately no map. The mechanics and rationale live in [the README's map section](../../README.md#finding-the-record-the-map); this record holds what was rejected.

## What we rejected

- **Co-location** — put each record next to the code it describes (`src/parser/CONTEXT.md`) and let proximity do the routing. It works until a record spans subsystems or describes something with no single home — a cross-cutting decision, a project-wide convention — and it trades one browsable folder of records for a scatter you can't survey at a glance. The map keeps the records together and still routes.
- **Scope-tags** — each record declares the paths it governs in front-matter (`scope: src/parser/**`), and a tool maps a changed file to its records. It is the most mechanically precise option, and it is the most structure: a required field on every record, which cuts against PCR's prose-first, no-fixed-format stance. The map buys most of the same routing with none of the schema. If real use ever proves the map insufficient at scale, scope-tags are where to go next — but start with the lighter thing.
- **A map from day one** — an earlier draft made the map mandatory, with setup creating a stub so the adoption block could say "start from the map" unconditionally. Rejected: a map over three records is ceremony — structure paid for before it returns anything — and PCR's own rule is that structure is added when real use demands it. The block routes through the map only when one exists.
- **Nothing, ever** — trust titles and a good folder listing at any size. Right at a handful of records (that is exactly the pre-map state), but at scale the agent is back to guessing, which is the failure the map exists to remove.

Related: [distill-draft](./distill-draft.md) (the audit that keeps the map honest), [freshness](./freshness.md).
