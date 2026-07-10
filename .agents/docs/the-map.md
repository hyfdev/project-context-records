# Retrieval: why a map file, not co-location or scope-tags

"Read the relevant record" is empty unless something routes an agent from the code in front of it to the exact context that bears on it. File count is a poor proxy: one long ledger can already be harder to search than a folder of short, well-named records.

## The decision

Once finding exact context stops being a glance, retrieval runs through one privileged record: `.agents/docs/README.md`, the map. The trigger can be many files, one long ledger, ambiguous titles, or [enrolled records](./existing-docs.md) outside the folder. Each route names the code area or hotspot, links the exact record or heading, and gives a one-line gist. A dense record can appear through multiple heading links. The map routes; content stays in the records.

Before that point, filenames remain the index; a map over three short records is ceremony. PCR adds structure when retrieval demands it, not at a fixed count.

The map is a distilled record, never an accumulated one — you don't pour notes into it, you promote a route once context is worth finding — and it can be vouched like any other. Its upkeep is still cheaper than re-reading every record, but not wholly mechanical: links can break, records or headings can go unlisted, and a code-area route can become wrong even while every file still exists. Normal changes and distillation check all three.

For narrow hotspots, code routes back to context with a one-line breadcrumb such as `// why: see .agents/docs/parser.md#error-recovery`. The map gets a reader from a task area to the right part of the archive; the breadcrumb fires at the exact implementation site.

## What we rejected

- **Co-locating every record** — put each record next to the code it describes (`src/parser/CONTEXT.md`) and let proximity do all the routing. It works until a record spans subsystems or describes something with no single home — a cross-cutting decision, a project-wide convention — and it trades one browsable folder of records for a scatter you can't survey at a glance. A short code breadcrumb keeps the useful local trigger without scattering the archive.
- **Scope-tags** — each record declares the paths it governs in front-matter (`scope: src/parser/**`), and a tool maps a changed file to its records. It is the most mechanically precise option, and it is the most structure: a required field on every record, which cuts against PCR's prose-first, no-fixed-format stance. The map buys most of the same routing with none of the schema. If real use ever proves the map insufficient at scale, scope-tags are where to go next — but start with the lighter thing.
- **A map from day one** — an earlier draft made the map mandatory, with setup creating a stub so the adoption block could say "start from the map" unconditionally. Rejected: a map over three short, obvious records is ceremony — structure paid for before it returns anything — and PCR's own rule is that structure is added when real use demands it. The block routes through the map only when one exists.
- **Nothing, ever** — trust titles and a good folder listing at any size. Right at a handful of records (that is exactly the pre-map state), but at scale the agent is back to guessing, which is the failure the map exists to remove.

Related: [records and enforcement](./records-vs-enforcement.md), [distill-draft](./distill-draft.md) (the review that keeps routes honest), [freshness](./freshness.md).
