# Engineering structure

Which files engineering owns, the test a document passes to enter one, where it goes, how an overtaken document is
changed, and what is deliberately absent. The layout they sit in is [layout.md](./layout.md).

## Engineering areas (ereq:areas)

Engineering owns these files in any folder under `work/`, and a file's name promises that everything in it is that
thing:

| File             | Promise                                                                                                                                    | Not this                                                                                    |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------- |
| `engineering.md` | What engineering commits to for this epic or initiative, constraints included, one `engineering:` record each (`ereq:requirement-record`). | Design; product intent, which lives upstream; documentation of what is built                |
| `assumptions.md` | The `assume:` records this folder's requirements rest on (`ereq:assumption-record`).                                                       | Requirements; product intent that has been stated                                           |
| `spec.md`        | The technical contracts answering this folder's requirements (`ereq:spec-contracts`).                                                      | Implementation progress; documentation of what is built, which is the owning project repo's |
| `slices/`        | The ordered changes that build the epic, one file each, derived from its requirements and spec (`ereq:slice-files`).                       | Facts of their own; progress, which the work tracker owns                                   |

At the root engineering owns only `engineering.md`, holding the constraints that bind the whole system; program-wide
engineering decisions go in the root `decisions.md`. It may also write the `epic.md` of an epic planned in a tracker,
which the shared `ereq:tracker-epic` rule in [layout.md](./layout.md) shapes.

## Document admission (ereq:document-admission)

<!-- shared:document-admission -->

A new document lands only if it owns a distinct subject no existing document owns — otherwise improve that one; has a
read-trigger, a question a reader arrives with — otherwise its content belongs in an existing document; takes the name
and place the layout gives it, or is linked in the same change from the document owning its subject; and retires what it
supersedes, which is corrected in place or deleted.

<!-- /shared:document-admission -->

## Placement (ereq:placement)

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

## Changing in place (ereq:change-in-place)

<!-- shared:change-in-place -->

When a decision or a later document overtakes a document, a passage, or a record, rewrite it in place in the same change
to say what now holds; when it no longer applies at all, delete it. Either way, the same change rewrites or removes
every citation of an id that no longer exists, so no citation is left dangling. Git history keeps the old version, and
nothing in the repo marks content as stale. Decisions follow their own format instead, and a folder in `delivered/` is
frozen: later work cites it and never rewrites it.

<!-- /shared:change-in-place -->

A requirement that no longer binds is deleted (`ereq:requirement-removal`), and a settled assumption with it
(`ereq:assumption-lifecycle`).

## Deliberately absent (ereq:deliberately-absent)

<!-- shared:deliberately-absent -->

These are missing on purpose; do not add them. There is no `product/` or `engineering/` root, because work is organized
by epic. There is no folder per service, component, or system area; a shared capability is an epic of its own. There is
no status folder other than `delivered/`: progress lives in frontmatter and the work tracker, and the one move finished
work makes is one way. There is no `contracts/` folder; a shared contract lives with the epic owning its capability.
There is no separate questions file: clarifying questions sit in the file they concern and deferred calls are open
decisions. There is no `index.md` anywhere: a work folder's front door is its `epic.md` or `initiative.md`, a document
folder is only its leaves, and the layout plus a listing says what each folder holds.

<!-- /shared:deliberately-absent -->
