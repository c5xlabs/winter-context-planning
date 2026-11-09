# Product id namespaces

The stable ids product content mints and cites, and the ids it never cites. Rule ids (`preq:`) live only in this
framework; content never cites them.

## Id namespaces (preq:id-namespaces)

Every product id belongs to exactly one namespace, and each namespace has one canonical home — the file holding the id's
defining row, section, or record, relative to the repo root. `preq:repository-entry` in
[`./repository-entry.md`](./repository-entry.md) covers homes outside the repo.

| Prefix        | Names                                                                            | Canonical home                                                                                                                             |
| ------------- | -------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| `persona:`    | A person the product serves                                                      | Row in `charter/personas.md`, or the persona's leaf in `charter/personas/` (`preq:persona-registry`)                                       |
| `job:`        | Something a person is trying to accomplish                                       | Row in `charter/jobs.md`                                                                                                                   |
| `initiative:` | A durable product investment broader than one capability                         | Row in `initiatives.md`                                                                                                                    |
| `epic:`       | A major capability the product must establish, `<epic>` or `<initiative>/<epic>` | The epic's `epic.md`, under `work/` or `delivered/`; `epics.md` lists the live ones                                                        |
| `product:`    | A product requirement of an epic, or one binding every epic of an initiative     | `## <Name> (product:<subject>)` heading in the owner's `requirements.md`, or `###` in `epic.md` when inline (`preq:requirement-records`)   |
| `milestone:`  | A destination visible in a person's work                                         | `## <Name> (milestone:<slug>)` section in `milestones.md`, or in `delivered.md` once reached                                               |
| `decision:`   | A decision of either tier, open or made                                          | `## <Name> (decision:…)` heading in the owner's `decisions.md`, shared with engineering (`preq:decision-slugs`, `preq:decision-ownership`) |

A fact that would still be true for a different product belongs in this framework, not in the repo.

## Slugs, not numbers (preq:slugs-not-numbers)

<!-- shared:slugs-not-numbers -->

Every id this tier mints is built from lowercase kebab-case slugs naming its subject, joined by `/` where it is scoped —
never a number, never date-prefixed, never reused once deleted. Replacing the thing an id names takes a new id. Subject
slugs need no allocation, so parallel authors collide only when they name the same thing.

<!-- /shared:slugs-not-numbers -->

## Stable product ids (preq:stable-product-ids)

Never rename or reuse a `persona:`, `job:`, `initiative:`, or `milestone:` slug, an epic's own slug, or a `product:`
subject: these ids are cited from trackers, other repos, and people, and none of those citations update. An epic id
changes only when the epic moves into or out of an initiative (`preq:moving-ids`). A product id's defining row, heading,
or frontmatter entry leaves only through a decision. A deleted subject keeps its slug out of circulation.

## Owned and scoped ids (preq:owned-scoped-ids)

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

Owners are initiatives and epics, and a `decision:` or `product:` id may belong to either; a `product:` subject names
what the requirement requires. The program is the program-wide owner and holds no `product:`: program-wide product
direction is the charter's, so there is no root `requirements.md`, and a bare `product:` resolves no further out than
its initiative.

## Bare ids (preq:bare-ids)

<!-- shared:bare-ids -->

A `product:`, `engineering:`, or `assume:` id may be written bare, as its subject alone, and the heading defining it
always carries the bare subject, since its folder supplies the scope. A bare id resolves like a scoped variable: first
in the work folder holding the citing file, a document folder such as `spec/` counting as part of it, then in each
enclosing initiative folder outward, then at the root; the first that defines the subject wins, never a folder further
in, and a bare id no level defines is read as a full id. The full form is valid everywhere.

**Detect.** A defining heading carrying a full id; a bare citation that no level from the citing folder outward defines.

<!-- /shared:bare-ids -->

## Moving ids (preq:moving-ids)

<!-- shared:moving-ids -->

Moving an epic into or out of an initiative changes the epic's id and every id scoped to it, and the change that moves
it rewrites every full citation in the repo and every bare one inside its folder that resolved to the initiative it
leaves; other bare ids stay as they are. A record changing owner is deleted from its old owner's file and written under
a new id in its new owner's, in a change that rewrites every citation. Citations outside the repo do not update when an
id moves or is deleted, and that is the accepted cost, so make a move deliberately.

**Detect.** After a move, a citation in the repo still carrying the old scope.

<!-- /shared:moving-ids -->

## Id citations and headings (preq:id-citations)

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

An id whose home is outside the repo is cited the same way; the Defined in column of the README's Ids table says where
to look it up.

## Product cites only product (preq:product-cites-product)

Product-owned files — the charter, the registries, `epic.md`, `initiative.md`, `requirements.md`, and mockups — cite
only product ids and the external homes the README declares for them, never an `engineering:` or `assume:` id, and never
link an engineering file. Any file may cite any `decision:`. Engineering derives from product and cites it; the reverse
would tie product intent to one implementation, go stale whenever engineering changes, and break in a repo holding no
engineering content. A requirement's acceptance bullets (`preq:requirement-acceptance` in
[`./requirements.md`](./requirements.md)) say what product judges it by, not the engineering records serving it. The
shared files — `decisions.md` and the `epic.md` of an epic planned in a tracker — follow their shared rules instead.
