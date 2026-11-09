# Product structure

Which files product owns, the test a document passes to enter one, where it goes, how an overtaken document is changed,
and what is deliberately absent. The layout they sit in is [`./layout.md`](./layout.md).

## Product areas (preq:areas)

Product owns these areas, and an area's name promises that everything in it is that thing. R = required when the repo
holds product content; O = optional. Root paths are relative to the repo root; folder files sit in a folder under
`work/`.

| Area                                                          | R/O                       | Promise                                                                                                                                                                                               | Not this                                                                                                |
| ------------------------------------------------------------- | ------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| `charter/`                                                    | R                         | The standing product direction: mission, vision, and the `persona:` and `job:` registries ([`./charter.md`](./charter.md)).                                                                           | Epic-level intent                                                                                       |
| `initiatives.md`, `epics.md`, `milestones.md`, `delivered.md` | R (`initiatives.md` O)    | The live registries and the delivery ledger, at the root ([`./registries.md`](./registries.md)).                                                                                                      | Work-item workflow, which is the work tracker's                                                         |
| `epic.md`                                                     | R in an epic folder       | The folder's front door: the epic's frontmatter, problem, outcome, and Left for later; its requirement records too when it has no `requirements.md` ([`./intent.md`](./intent.md)).                   | Technical design — sequence diagrams, schemas, endpoint contracts; program-wide direction; raw analysis |
| `initiative.md`                                               | R in an initiative folder | The folder's front door: the initiative's frontmatter, problem, outcome, and Left for later ([`./intent.md`](./intent.md)).                                                                           | Its epics' intent; technical design                                                                     |
| `requirements.md`                                             | O                         | In an epic folder, one `product:` record per requirement with its acceptance bullets; in an initiative folder, only requirements binding every epic in it ([`./requirements.md`](./requirements.md)). | The problem and outcome, which are `epic.md`'s; technical design                                        |
| `mockups/`                                                    | O                         | In a work folder, the mockups for that epic, or for several epics of that initiative ([`./mockups.md`](./mockups.md)).                                                                                | The kit                                                                                                 |
| `strategy/`                                                   | O                         | At the root, direction-setting papers — program intent, framing, and priorities. Few, long-lived, heavily cited.                                                                                      | Intent for one initiative or epic; research findings                                                    |
| `mockup-kit/`                                                 | O                         | At the root, the stylesheet and brand marks mockups share, with the kit README ([`./mockups.md`](./mockups.md)).                                                                                      | The mockups themselves, which live with their work                                                      |

Technical design stays out of the product files because it serves the implementer and drifts at a different rate from
product intent. Use nested epics only when part of an initiative's investment has its own focused promise.

## Document admission (preq:document-admission)

<!-- shared:document-admission -->

A new document lands only if it owns a distinct subject no existing document owns — otherwise improve that one; has a
read-trigger, a question a reader arrives with — otherwise its content belongs in an existing document; takes the name
and place the layout gives it, or is linked in the same change from the document owning its subject; and retires what it
supersedes, which is corrected in place or deleted.

<!-- /shared:document-admission -->

## Placement (preq:placement)

<!-- shared:placement -->

Place a document by the question its reader arrives with, not by the work or team that produced it. Research groups by
subject, not consumer, because it outlives the work that commissioned it and is cited by more than one owner; a script
stays beside the findings it produced so the result can be re-derived. When several documents misfit the area they sit
in, rename the area to name the real boundary and repoint the routers — never widen the area's promise to cover the
misfits.

<!-- /shared:placement -->

<!-- shared:placement-routes -->

| Reader asks                                       | Goes in                                                                                                               |
| ------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| What are we trying to achieve?                    | `strategy/`                                                                                                           |
| Why does this work exist, and what will change?   | The owning folder's `epic.md` or `initiative.md`                                                                      |
| What are we building, and how will people use it? | The epic's `requirements.md`, or its `epic.md` when the requirement records are inline                                |
| What must the system do?                          | The owning folder's `engineering.md`; the root's for a constraint on the whole system                                 |
| What are we assuming?                             | The `assumptions.md` of the folder whose requirements rest on it                                                      |
| How is it built?                                  | The epic folder's `spec.md`, or its `spec/` in folder form                                                            |
| In what steps is it built?                        | The epic folder's `slices/`                                                                                           |
| What did we learn?                                | The owning folder's `research/` when local to it, otherwise the root `research/<subject>/`                            |
| What did we settle, or leave to decide?           | The owning folder's `decisions.md`; the root `decisions.md` for calls across epics or that no epic or initiative owns |
| What did this mean?                               | The `## Open questions` at the end of the file it concerns                                                            |

<!-- /shared:placement-routes -->

<!-- shared:placement-why -->

Each reader question has exactly one place its answer goes.

<!-- /shared:placement-why -->

## Changing in place (preq:change-in-place)

<!-- shared:change-in-place -->

When a decision or a later document overtakes a document, a passage, or a record, rewrite it in place in the same change
to say what now holds; when it no longer applies at all, delete it. Either way, the same change rewrites or removes
every citation of an id that no longer exists, so no citation is left dangling. Git history keeps the old version, and
nothing in the repo marks content as stale. Decisions follow their own format instead, and a folder in `delivered/` is
frozen: later work cites it and never rewrites it.

<!-- /shared:change-in-place -->

## Deliberately absent (preq:deliberately-absent)

<!-- shared:deliberately-absent -->

These are missing on purpose; do not add them. There is no `product/` or `engineering/` root, because work is organized
by epic. There is no folder per service, component, or system area; a shared capability is an epic of its own. There is
no status folder other than `delivered/`: progress lives in frontmatter and the work tracker, and the one move finished
work makes is one way. There is no `contracts/` folder; a shared contract lives with the epic owning its capability.
There is no separate questions file: clarifying questions sit in the file they concern and deferred calls are open
decisions. There is no `index.md` anywhere: a work folder's front door is its `epic.md` or `initiative.md`, a document
folder is only its leaves, and the layout plus a listing says what each folder holds.

<!-- /shared:deliberately-absent -->
