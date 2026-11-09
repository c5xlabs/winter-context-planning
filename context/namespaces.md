# Ids

The stable ids product and engineering content mint and cite, how a scope and a project enter them, how they resolve,
and which ids product never cites. Rule ids (`planning:`) live only in this framework; content never cites them.

## Id namespaces (planning:id-namespaces)

Every stable id belongs to exactly one namespace, and each namespace has one canonical home — the file holding the id's
defining row, section, or record, relative to the repo root. `planning:repository-entry` in
[`./repository-entry.md`](./repository-entry.md) covers homes outside the repo. Product's prefixes and engineering's are
disjoint except `decision:`, which both tiers share under one subject rule (`planning:decision-slugs` in
[`./decisions.md`](./decisions.md)), so both tiers share a folder without colliding.

| Prefix         | Tier        | Names                                                                                      | Canonical home                                                                                                                               |
| -------------- | ----------- | ------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------- |
| `persona:`     | Product     | A person the product serves                                                                | Row in a charter's `personas.md`, or the persona's leaf in its `personas/` (`planning:persona-registry`)                                     |
| `job:`         | Product     | Something a person is trying to accomplish                                                 | Row in a charter's `jobs.md`                                                                                                                 |
| `initiative:`  | Product     | A durable product investment broader than one capability                                   | Row in `initiatives.md`                                                                                                                      |
| `epic:`        | Product     | A major capability the product must establish, `<epic>` or `<initiative>/<epic>`           | The epic's `epic.md`, under `work/` or `delivered/`; `epics.md` lists the live ones                                                          |
| `product:`     | Product     | A product requirement of an epic, or one binding every epic of its owner                   | `## <Name> (product:<subject>)` heading in the owner's `requirements.md`, or `###` in `epic.md` when inline (`planning:requirement-records`) |
| `milestone:`   | Product     | A destination visible in a person's work                                                   | `## <Name> (milestone:<slug>)` section in a `milestones.md`, or in the `delivered.md` beside it once reached                                 |
| `engineering:` | Engineering | What engineering commits to, `<owner id>/<subject>` or bare, always bare at the root       | `## <Name> (engineering:<subject>)` heading in the owning folder's, or the root's, `engineering.md`                                          |
| `assume:`      | Engineering | Product intent engineering assumed because none was stated, `<owner id>/<subject>` or bare | `## <Name> (assume:<subject>)` heading in the `assumptions.md` of the folder whose requirements rest on it                                   |
| `decision:`    | Both        | A decision of either tier, open or made, always written in full                            | `## <Name> (decision:…)` heading in the owner's `decisions.md` (`planning:decision-slugs`, `planning:decision-ownership`)                    |

Upstream ids — the product intent an engineering requirement derives from — use the schemes of
`planning:upstream-schemes` in [`./derivation.md`](./derivation.md), not namespaces minted here. A fact that would still
be true for a different product belongs in this framework, not in the repo.

## Slugs, not numbers (planning:slugs-not-numbers)

Every id this tier mints is built from lowercase kebab-case slugs naming its subject, joined by `/` where it is scoped —
never a number, never date-prefixed, never reused once deleted. Replacing the thing an id names takes a new id. Subject
slugs need no allocation, so parallel authors collide only when they name the same thing.

## Stable product ids (planning:stable-product-ids)

Never rename or reuse a `persona:`, `job:`, `initiative:`, or `milestone:` slug, an epic's own slug, or a `product:`
subject: these ids are cited from trackers, other repos, and people, and none of those citations update. An epic id
changes only when the epic moves into or out of an initiative (`planning:moving-ids`). A product id's defining row,
heading, or frontmatter entry leaves only through a decision. A deleted subject keeps its slug out of circulation.

## Owned and scoped ids (planning:owned-scoped-ids)

An epic's id is `<epic>` when it stands alone and `<initiative>/<epic>` under an initiative, since two initiatives may
each hold an epic of the same name; an initiative's id is its slug. An id an owner holds is
`<prefix>:<owner id>/<subject>` — `engineering:reliable-borrowing/reservations/confirmed-event-consumption` — and the
last segment is always the subject. A record binding the whole program has no scope —
`engineering:written-in-typescript` in the root `engineering.md`. Decision ids are always written in full, and one with
no scope is program-wide; never add a filler scope to one. Ids never name the `work/`, `delivered/`, or `projects/`
folder, so delivery moves nothing in them.

**Detect.** An id naming `work/`, `delivered/`, or `projects/`; a decision id written bare or given a filler scope.

Product's owners are epics, initiatives, and the program, and a `decision:` or `product:` id may belong to any of them;
a `product:` subject names what the requirement requires. The program's `product:` records, in the root
`requirements.md`, bind every epic in it, and their ids are always bare. Program-wide direction — who the product serves
and why it exists — stays the charter's; a program requirement is a promise every epic must keep.

Engineering's owners are the same, and a scoped owner id is an epic id — `<epic>` or `<initiative>/<epic>` — or an
initiative slug. The program's `engineering:` records bind the whole system (`planning:engineering-constraints` in
[`./engineering.md`](./engineering.md)) and are always bare; an unscoped `decision:` is program-wide. The program holds
no `assume:`: an assumption sits beside the requirements resting on it, inside the work.

In a repo with projects (`planning:projects` in [`./projects.md`](./projects.md)), a project is an owner between the
program and its initiatives, and its slug is the first segment of every id it scopes: `epic:fleet/board`,
`epic:fleet/reliability/hub`, `product:fleet/board/live-status`, `engineering:fleet/written-in-go`,
`decision:fleet/board/column-order`, `initiative:fleet/reliability`, `persona:fleet/operator`,
`milestone:fleet/first-run`. A record binding the whole project is scoped by the project alone. Program records stay
unscoped — `persona:developer`, `product:stable-json` — and a first segment that is a project slug always names that
project (`planning:project-slugs` in [`./projects.md`](./projects.md)).

## Bare ids (planning:bare-ids)

A `product:`, `engineering:`, or `assume:` id may be written bare, as its subject alone, and the heading defining it
always carries the bare subject, since its folder supplies the scope. A bare id resolves like a scoped variable: first
in the work folder holding the citing file, a document folder such as `spec/` counting as part of it, then in each
enclosing initiative folder outward, then in the project folder when there is one, then at the root; the first that
defines the subject wins, never a folder further in, and a bare id no level defines is read as a full id. The full form
is valid everywhere.

Inside a project, every id the project scopes may also drop its project segment — `epic:board`, `persona:operator`,
`decision:board/column-order` inside `fleet` — and resolves in the citing file's project first, then at the program.
Frontmatter and defining headings inside a project write ids in this project-relative form, since the folder supplies
the project. Outside its project, an id always carries it: a `workspace` file cites `epic:fleet/board`, never
`epic:board`.

**Detect.** A defining heading carrying a full id; a bare citation that no level from the citing folder outward defines;
a citation dropping the project segment of an id another project scopes.

## No shadowing (planning:no-shadowing)

An inner level never defines an id an enclosing level already defines: no epic or initiative reuses a `product:`,
`engineering:`, or `assume:` subject its initiative, project, or the program holds, and no project mints a `persona:`,
`job:`, `milestone:`, or `decision:` slug the program holds. Resolution stops at the innermost definition, so a shadowed
outer record could no longer be cited from inside the level hiding it, and two records naming the same subject on one
path are one record written twice. Before minting, check every level outward from the folder that will hold the id.

**Detect.** The same subject defined at two levels on one path from a work folder to the root.

## Moving ids (planning:moving-ids)

Moving an epic into or out of an initiative, or an epic or initiative from one project to another, changes its id and
every id scoped to it, and the change that moves it rewrites every full citation in the repo and every bare or
project-relative one inside its folder that resolved to the level it leaves; other bare ids stay as they are. Promoting
a project's persona, job, or milestone to the program, once more than one project needs it, is a move of the same kind
(`planning:cross-project` in [`./projects.md`](./projects.md)). A record changing owner is deleted from its old owner's
file and written under a new id in its new owner's, in a change that rewrites every citation. Citations outside the repo
do not update when an id moves or is deleted, and that is the accepted cost, so make a move deliberately.

**Detect.** After a move, a citation in the repo still carrying the old scope or project.

## Id citations and headings (planning:id-citations)

Cite an id as plain text, the id alone in backticks — `` `persona:member` `` — never as a markdown link; the one id that
is a link is a registry row's own, which links the document owning it. Every id appears verbatim at its home, the row,
heading, or frontmatter field defining it, so a reader finds the home by searching for the id; an id at its home is not
a citation. A heading that defines an id names the record, then carries the id in parentheses, in its bare form where it
has one and without backticks: `## Volunteers per shift (decision:volunteer-shifts/volunteers-per-shift)`,
`## Cover expiry (engineering:cover-expiry)`. No heading is ever an id alone. In a file that exists to hold records,
such as `decisions.md` or `assumptions.md`, each record is a `##` section; where records sit beside a file's own
sections, as requirement records inline in `epic.md` do, they gather under a `## Requirements` heading, each a `###`
section. Any other link points at a document rather than citing an id, and stays a link.

An id whose home is outside the repo is cited the same way; the Defined in column of the README's Ids table says where
to look it up. This covers prose, tables, and code comments. A scheme id (`product:`, `jira:`, …) is cited the same way,
and a reader resolves it through the README's scheme table, never against a base the table does not declare.

## Product cites only product (planning:product-cites-product)

Product-owned files — the charter, the registries, `epic.md`, `initiative.md`, `requirements.md`, and mockups — cite
only product ids and the external homes the README declares for them, never an `engineering:` or `assume:` id, and never
link an engineering file. Any file may cite any `decision:`. Engineering derives from product and cites it; the reverse
would tie product intent to one implementation, go stale whenever engineering changes, and break in a repo holding no
engineering content. A requirement's acceptance bullets (`planning:requirement-acceptance` in
[`./requirements.md`](./requirements.md)) say what product judges it by, not the engineering records serving it. The
shared files — `decisions.md` and the `epic.md` of an epic planned in a tracker — follow their shared rules instead.
