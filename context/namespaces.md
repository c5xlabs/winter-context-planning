# Ids

The stable ids product and engineering content mint and cite: how they are built and scoped, how they resolve and move,
and which ones product may cite. Rule ids (`planning:`) belong to this framework alone; content never cites them.

## Id namespaces (planning:id-namespaces)

Every stable id belongs to one namespace, and each namespace has one home: the file holding the id's defining row,
section, or record. Homes outside the repo are covered in [`./repository-entry.md`](./repository-entry.md). Product and
engineering use disjoint prefixes, except `decision:`, which both share.

| Prefix         | Tier        | Names                                                            | Home                                                                              |
| -------------- | ----------- | ---------------------------------------------------------------- | --------------------------------------------------------------------------------- |
| `persona:`     | Product     | A person the product serves                                      | A row in a charter's `personas.md`, or a leaf in its `personas/`                  |
| `job:`         | Product     | Something a person is trying to accomplish                       | A row in a charter's `jobs.md`                                                    |
| `initiative:`  | Product     | A durable investment broader than one capability                 | A row in `initiatives.md`                                                         |
| `epic:`        | Product     | A major capability the product must establish                    | The epic's `epic.md`, under `work/` or `delivered/`; `epics.md` lists live ones   |
| `product:`     | Product     | A requirement of an epic, or one binding every epic of its owner | A heading in the owner's `requirements.md`, or inline in `epic.md`                |
| `milestone:`   | Product     | A destination visible in a person's work                         | A section in a `milestones.md`, then in the `delivered.md` beside it once reached |
| `engineering:` | Engineering | What engineering commits to                                      | A heading in the owning folder's, or the root's, `engineering.md`                 |
| `assume:`      | Engineering | Product intent engineering assumed because none was stated       | A heading in the `assumptions.md` beside the requirements resting on it           |
| `decision:`    | Both        | A decision of either tier, open or made                          | A heading in the owner's [`decisions.md`](./decisions.md)                         |

Upstream ids, naming the product intent an engineering requirement derives from, use the schemes in
[`./derivation.md`](./derivation.md) rather than a namespace minted here. A fact that would still be true for a
different product belongs in this framework, not in the repo.

## Slugs, not numbers (planning:slugs-not-numbers)

Ids are built from lowercase kebab-case slugs naming their subject, joined by `/` where scoped. No numbers, no date
prefixes, and no reusing a deleted id: replacing the thing an id names takes a new id.

## Stable product ids (planning:stable-product-ids)

Never rename a `persona:`, `job:`, `initiative:`, or `milestone:` slug, an epic's own slug, or a `product:` subject.
Trackers, other repos, and people cite them, and those citations never update. An epic's id changes only when the epic
moves into or out of an initiative. A product id's definition is removed only through a decision, and its slug stays
retired.

## Owned and scoped ids (planning:owned-scoped-ids)

An epic's id is `<epic>` when it stands alone and `<initiative>/<epic>` under an initiative; an initiative's id is its
slug. An id an owner holds is `<prefix>:<owner id>/<subject>`, as in
`engineering:reliable-borrowing/reservations/confirmed-event-consumption`, and the last segment is always the subject.
Ids never name the `work/`, `delivered/`, or `projects/` folder, so delivery changes no id.

In both tiers the owners are epics, initiatives, and the program. The program's records bind everything in it and are
never scoped: its `product:` records in the root `requirements.md` are promises every epic must keep, and its
`engineering:` records in the root [`engineering.md`](./engineering.md) bind the whole system, as
`engineering:written-in-typescript` does. Who the product serves and why it exists stays in the charter. The program
holds no `assume:`; an assumption sits beside the requirements resting on it. A `product:` subject names what the
requirement requires.

Decision ids are always written in full. One with no scope is program-wide; never give it a filler scope.

In a repo with [projects](./projects.md), a project is an owner between the program and its initiatives, and its slug is
the first segment of every id it scopes: `epic:fleet/board`, `epic:fleet/reliability/hub`,
`product:fleet/board/live-status`, `engineering:fleet/written-in-go`, `decision:fleet/board/column-order`,
`initiative:fleet/reliability`, `persona:fleet/operator`, `milestone:fleet/first-run`. A record binding the whole
project is scoped by the project alone. Program records stay unscoped (`persona:developer`, `product:stable-json`), and
a first segment that is a project slug always names that project.

## Bare ids (planning:bare-ids)

A `product:`, `engineering:`, or `assume:` id may be cited bare, as its subject alone, and its defining heading always
uses the bare subject, since the folder supplies the scope. A bare id resolves like a scoped variable: first in the work
folder holding the citing file (a document folder such as `spec/` counts as part of it), then in each enclosing
initiative folder outward, then in the project folder if there is one, then at the root. The first level that defines
the subject wins. A bare id that no level defines is read as a full id, and the full form is valid everywhere.

Inside a project, any id the project scopes may also drop its project segment (`epic:board`, `persona:operator`,
`decision:board/column-order` inside `fleet`) and resolves in the citing file's project first, then at the program.
Frontmatter and defining headings inside a project use this project-relative form. Outside its project an id always
carries the project: a `workspace` file cites `epic:fleet/board`, never `epic:board`.

## No shadowing (planning:no-shadowing)

An inner level never defines an id an enclosing level already defines. No epic or initiative reuses a `product:`,
`engineering:`, or `assume:` subject held by its initiative, its project, or the program, and no project mints a
`persona:`, `job:`, `milestone:`, or `decision:` slug the program holds. Before minting, check every level from the id's
folder out to the root.

## Moving ids (planning:moving-ids)

Moving an epic into or out of an initiative, or an epic or initiative to another project, changes its id and every id
scoped to it. The change that moves it rewrites every full citation in the repo, and every bare or project-relative
citation inside the moved folder that resolved to the level it leaves; other bare ids stay as they are. Promoting a
project's persona, job, or milestone to the program once more than one project needs it is the same kind of move.

A record changing owner is deleted from the old owner's file and written under a new id in the new owner's, in one
change that rewrites every citation. Citations outside the repo never update, so move deliberately.

## Id citations and headings (planning:id-citations)

Cite an id as plain text in backticks, `` `persona:member` ``, never as a markdown link. The one exception is a registry
row's own id, which links the document owning it. Every id appears verbatim at its home, so searching for it finds the
definition.

A heading that defines an id names the record, then gives the id in parentheses, bare where it has a bare form and
without backticks: `## Volunteers per shift (decision:volunteer-shifts/volunteers-per-shift)`,
`## Cover expiry (engineering:cover-expiry)`. No heading is an id alone. In a file that exists to hold records, such as
`decisions.md` or `assumptions.md`, each record is a `##` section. Records inline in `epic.md` gather under a
`## Requirements` heading, each a `###` section.

Ids homed outside the repo are cited the same way, in prose, tables, and code comments alike; the README's Ids table
says where each is defined. A scheme id (`product:`, `jira:`, …) resolves through the README's scheme table, never
against a base the table doesn't declare.

## Product cites only product (planning:product-cites-product)

Product-owned files (the charter, the registries, `epic.md`, `initiative.md`, `requirements.md`, and mockups) cite only
product ids and the external homes the README declares for them. They never cite an `engineering:` or `assume:` id and
never link an engineering file. Any file may cite any `decision:`. A requirement's acceptance bullets say what product
judges it by, not which engineering records serve it. `decisions.md` and the `epic.md` of an epic planned in a tracker
are shared files and follow their own rules.
