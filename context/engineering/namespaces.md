# Engineering ids

The stable ids engineering content mints and cites. Rule ids (`ereq:`) live in this framework and never appear in
content.

## Id namespaces (ereq:id-namespaces)

Every stable id engineering content mints belongs to one namespace, with one canonical home — the record or row that
defines it. Engineering's prefixes are disjoint from product's except `decision:`, which both tiers share under one
subject rule (`ereq:decision-slugs` in [decisions.md](./decisions.md)), so both tiers share a folder without colliding.

| Prefix         | Names                                                      | Format                                                                                     | Canonical home                                                                                                                         |
| -------------- | ---------------------------------------------------------- | ------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------- |
| `engineering:` | What engineering commits to                                | `engineering:<owner id>/<subject>`, or bare `engineering:<subject>`, always so at the root | `## <Name> (engineering:<subject>)` heading in the owning folder's, or the root's, `engineering.md`                                    |
| `assume:`      | Product intent engineering assumed because none was stated | `assume:<owner id>/<subject>`, or bare `assume:<subject>`                                  | `## <Name> (assume:<subject>)` heading in the `assumptions.md` of the folder whose requirements rest on it                             |
| `decision:`    | A decision of either tier, open or made                    | `decision:<owner id>/<subject>` or `decision:<subject>`, always in full                    | `## <Name> (decision:…)` heading in the owner's `decisions.md`, shared with product (`ereq:decision-slugs`, `ereq:decision-ownership`) |

Upstream ids — the product intent a requirement derives from — use the schemes of `ereq:upstream-schemes` in
[derivation.md](./derivation.md), not namespaces minted here.

## Slugs, not numbers (ereq:slugs-not-numbers)

<!-- shared:slugs-not-numbers -->

Every id this tier mints is built from lowercase kebab-case slugs naming its subject, joined by `/` where it is scoped —
never a number, never date-prefixed, never reused once deleted. Replacing the thing an id names takes a new id. Subject
slugs need no allocation, so parallel authors collide only when they name the same thing.

<!-- /shared:slugs-not-numbers -->

## Owned and scoped ids (ereq:owned-scoped-ids)

<!-- shared:owned-scoped-ids -->

An epic's id is `<epic>` when it stands alone and `<initiative>/<epic>` under an initiative, since two initiatives may
each hold an epic of the same name; an initiative's id is its slug. An id an owner holds is
`<prefix>:<owner id>/<subject>` — `engineering:reliable-borrowing/reservations/confirmed-event-consumption` — and the
last segment is always the subject. A record binding the whole program has no scope —
`engineering:written-in-typescript` in the root `engineering.md`. Decision ids are always written in full, and one with
no scope is program-wide; never add a filler scope to one. Ids never name the `work/` or `delivered/` root, so delivery
moves nothing in them.

**Detect.** An id naming `work/` or `delivered/`; a decision id written bare or given a filler scope.

<!-- /shared:owned-scoped-ids -->

Owners are epics, initiatives, and the program, and a scoped owner id is an epic id — `<epic>` or `<initiative>/<epic>`
— or an initiative slug. The program holds only the `engineering:` constraints binding the whole system
(`ereq:engineering-constraints` in [engineering.md](./engineering.md)), always bare, and never an `assume:`, since a
constraint rests on no assumption; an unscoped `decision:` is program-wide.

## Bare ids (ereq:bare-ids)

<!-- shared:bare-ids -->

A `product:`, `engineering:`, or `assume:` id may be written bare, as its subject alone, and the heading defining it
always carries the bare subject, since its folder supplies the scope. A bare id resolves like a scoped variable: first
in the work folder holding the citing file, a document folder such as `spec/` counting as part of it, then in each
enclosing initiative folder outward, then at the root; the first that defines the subject wins, never a folder further
in, and a bare id no level defines is read as a full id. The full form is valid everywhere.

**Detect.** A defining heading carrying a full id; a bare citation that no level from the citing folder outward defines.

<!-- /shared:bare-ids -->

## Moving ids (ereq:moving-ids)

<!-- shared:moving-ids -->

Moving an epic into or out of an initiative changes the epic's id and every id scoped to it, and the change that moves
it rewrites every full citation in the repo and every bare one inside its folder that resolved to the initiative it
leaves; other bare ids stay as they are. A record changing owner is deleted from its old owner's file and written under
a new id in its new owner's, in a change that rewrites every citation. Citations outside the repo do not update when an
id moves or is deleted, and that is the accepted cost, so make a move deliberately.

**Detect.** After a move, a citation in the repo still carrying the old scope.

<!-- /shared:moving-ids -->

## Id citations and headings (ereq:id-citations)

<!-- shared:id-citations -->

Cite an id as plain text, the id alone in backticks — `` `persona:member` `` — never as a markdown link; the one id that
is a link is a registry row's own, which links the document owning it. Every id appears verbatim at its home, the row,
heading, or frontmatter field defining it, so a reader finds the home by searching for the id; an id at its home is not
a citation. A heading that defines an id names the record, then carries the id in parentheses, in its bare form where it
has one and without backticks: `## Volunteers per shift (decision:volunteer-shifts/volunteers-per-shift)`,
`## Cover expiry (engineering:cover-expiry)`. No heading is ever an id alone. In a file that exists to hold records,
such as `decisions.md` or `assumptions.md`, each record is a `##` section; where records sit beside a file's own
sections, as requirement records inline in `epic.md` do, they gather under a `## Requirements` heading, each a `###`
section. Any other link points at a document rather than citing an id, and stays a link.

<!-- /shared:id-citations -->

This covers prose, tables, and code comments. A scheme id (`product:`, `jira:`, …) is cited the same way, and a reader
resolves it through the README's scheme table, never against a base the table does not declare.
