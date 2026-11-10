# Structure

What product and engineering keep beyond the work-folder files, when a new document earns a place, where it goes, how it
changes once overtaken, and what the repo leaves out on purpose. The files in a work folder, and which tier owns each,
are listed in `planning:layout`.

## Product areas (planning:product-areas)

An area's name is a promise that everything in it is that thing. Beyond its work-folder files, product owns these areas
at the root; the required ones are required once the repo holds any product content. In a repo with projects, the
program root and each project folder split them ([`./projects.md`](./projects.md)).

| Area                            | Required | Holds                                                                                                        |
| ------------------------------- | -------- | ------------------------------------------------------------------------------------------------------------ |
| `charter/`                      | Yes      | Mission, vision, and the `persona:` and `job:` registries ([`../product/charter.md`](../product/charter.md)) |
| `milestones.md`, `delivered.md` | Yes      | The milestone registry and the delivery ledger ([`../product/registries.md`](../product/registries.md))      |
| `strategy/`                     | No       | Direction-setting papers for the program                                                                     |
| `mockup-kit/`                   | No       | The stylesheet, brand marks, and README the mockups share ([`../product/mockups.md`](../product/mockups.md)) |

Strategy papers are few, long-lived, and heavily cited; intent for a single initiative or epic belongs in its folder,
and research findings in `research/`. Technical design, such as sequence diagrams, schemas, and endpoint contracts,
stays out of product files. Nest an epic only when part of an initiative's investment has its own focused promise.

## Engineering areas (planning:engineering-areas)

Slices are derived from the requirements and spec and add no facts of their own. Progress belongs to the work tracker
and documentation of what was built to the project repo that owns it; neither lives here. Product intent that has
already been stated is not an assumption.

At the root and in a project folder, engineering owns only `engineering.md`, for records that bind the whole program or
project, with their engineering decisions in the `decisions.md` beside it. Engineering may also write the `epic.md` of
an epic planned in a tracker, shaped by `planning:tracker-epic`.

## Document admission (planning:document-admission)

A new document lands only if:

- it owns a subject no existing document owns; otherwise, improve that one
- a reader arrives with a question it answers; otherwise, its content goes in an existing document
- it takes the name and place the layout gives it, or the document owning its subject links to it in the same change
- the same change corrects or deletes whatever it supersedes

## Placement (planning:placement)

Place a document by the question its reader arrives with, not by the work or team that produced it. Each question has
exactly one place its answer goes:

| Reader asks                                       | Goes in                                                                                |
| ------------------------------------------------- | -------------------------------------------------------------------------------------- |
| What are we trying to achieve?                    | `strategy/`                                                                            |
| Why does this work exist, and what will change?   | The owning folder's `epic.md` or `initiative.md`                                       |
| What are we building, and how will people use it? | The epic's `requirements.md`, or its `epic.md` when the records are inline             |
| What must the system do?                          | The owning folder's `engineering.md`                                                   |
| What are we assuming?                             | The `assumptions.md` of the folder whose requirements rest on it                       |
| How is it built?                                  | The epic folder's `spec.md`, or `spec/` in folder form                                 |
| In what steps is it built?                        | The epic folder's `slices/`                                                            |
| What did we learn?                                | The owning folder's `research/`, or the root `research/<subject>/` when it isn't local |
| What did we settle, or leave to decide?           | The owning folder's `decisions.md`                                                     |
| What did this mean?                               | The `## Open questions` at the end of the file it concerns                             |

A record or decision that binds a whole project or program, or that no single epic owns, goes in that project's or the
root's file. Root research is grouped by subject rather than by who asked for it, and a script stays beside the findings
it produced.

When several documents misfit their area, rename the area to name the real boundary and repoint the routers; don't widen
its promise to cover them.

## Changing in place (planning:change-in-place)

When a decision or a later document overtakes a document, passage, or record, rewrite it in the same change to say what
now holds, or delete it if it no longer applies. The same change rewrites or removes every citation of an id that no
longer exists. Nothing in the repo marks content as stale; git keeps the old version.

Two exceptions: decisions follow their own format, and a folder in `delivered/` is frozen, so later work cites it but
never rewrites it. A requirement that no longer binds is deleted (`planning:requirement-removal`), and so is an
assumption once it is settled (`planning:assumption-lifecycle`).

## Deliberately absent (planning:deliberately-absent)

The repo leaves these out on purpose; don't add them:

- A `product/` or `engineering/` root. Work is organized by epic.
- A folder per service, component, or system area. A shared capability is an epic of its own.
- A status folder other than `delivered/`. Progress lives in frontmatter and the work tracker, and moving to
  `delivered/` is one way.
- A `contracts/` folder. A shared contract lives with the epic that owns its capability.
- A separate questions file. Clarifying questions sit in the file they concern, and deferred calls are open decisions.
- An epic registry. The live epics are what `work/` contains, each `epic.md` is its epic's home, and milestone order
  says what comes first.
- An initiative registry. Each `initiative.md` is its initiative's home, and its `epics:` list names its epics.
- A project registry. The `projects/` listing and the README name the projects; a repo planning one product has no
  `projects/` folder.
- An `index.md` anywhere. A work folder's front door is its `epic.md` or `initiative.md`, and a document folder holds
  only its leaves.
