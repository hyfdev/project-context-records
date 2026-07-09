# Existing docs: enroll, don't migrate

Real repos — especially the mature ones PCR most wants — already hold pieces of the meta-layer under names the community standardized long before PCR: `DESIGN.md`, `ARCHITECTURE.md`, `adr/` folders, internal docs. The methodology has to say what happens to them at adoption, because the default failure is silent: seeding drafts an `architecture.md` next to an existing `ARCHITECTURE.md`, and the twins drift into contradiction — the exact trap PCR exists to prevent.

## The decision

Existing docs are **enrolled, not migrated**: a map row points at each where it lives, and from then on it follows the same rules as any record — kept fresh, stampable, updated in the same change that affects it. `.agents/docs/` is the default home for new records, not a wall around old ones. Seeding drafts only what no existing doc covers. The normative statement is in [the README's "What goes in"](../../README.md#what-goes-in).

## What we rejected

- **Migrate into the records folder** — breaks inbound links and GitHub discoverability (root `ARCHITECTURE.md` is where humans look), fights the community's conventions instead of building on them, and makes adoption heaviest for exactly the mature repos that have the most to enroll.
- **Ignore them** — seeding then manufactures twins, and agents treat the un-enrolled doc as scenery rather than a record they must keep fresh.

Related: [the-map](./the-map.md) (enrolled records outside the folder are the map's second trigger), [starter-set](./starter-set.md).
