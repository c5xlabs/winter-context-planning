# Engineering requirements

A work folder's `engineering.md` holds what engineering commits to, one record per `engineering:` id. Whether a
statement is engineering's to require at all is decided by `planning:classify-requirement`.

## Requirement ids (planning:requirement-ids)

A requirement's id is `engineering:<owner id>/<subject>`, where the owner is the epic, initiative, or project whose
folder holds it. A requirement the root holds is just `engineering:<subject>`. Bare ids resolve outward from the citing
folder (`planning:bare-ids`).

When an epic moves into or out of an initiative, its full ids change and every full citation is rewritten
(`planning:moving-ids`); bare citations inside the folder stay as they are. So
`engineering:overdue-returns/overdue-sweep` becomes `engineering:reliable-borrowing/overdue-returns/overdue-sweep` if
the epic moves under `reliable-borrowing`. Apart from that, an id is never renamed or reused.

A record moves only with its whole folder, as when it goes to `delivered/` and keeps its id. A record that turns out to
belong to another epic is deleted here and written there under a new id, in the same change that rewrites its citations
(`planning:requirement-removal`).

## Requirement records (planning:requirement-record)

Each requirement is a `##` section headed `<Name> (engineering:<subject>)`, followed by a sentence or two of what
engineering commits to. That is either a bound derived from a product promise, citing the intent it serves inline
(`planning:serves`), or a standalone constraint. Records have no fields and no "implemented" state; delivery is tracked
in the work tracker and the upstream intent. A record may open with **Proposed.**, which means what it does on a product
requirement (`planning:requirement-records`).

The record says what the behaviour is and why, in prose; the spec leaves that out (`planning:spec-contracts`). Write it
in the engineering voice (`planning:engineering-voice`). In folder form (`planning:file-or-folder`), each record is its
own `engineering/<subject>.md`, with no index.

```markdown
## Cover expiry (engineering:cover-expiry)

A stand-in's coordinator calls are refused within 60 seconds of the cover's end time, so the calls are back with the
coordinator when the product promises. Serves `product:coordinator-cover`.

Acceptance:

- A roster change the stand-in submits 61 seconds after the end time is refused.
```

## Beyond product (planning:beyond-product)

An engineering requirement never restates a product requirement; it says what engineering commits to beyond it, or it
isn't written.

Acceptance criteria are optional: a short `Acceptance:` list under the sentences, as on a product requirement. Each
bullet must be checkable by a test or a measurement, so words like "should", "fast", or "user-friendly" don't belong. A
criterion a user would notice, such as what the member is told, what the volunteer sees, or how soon, belongs under the
`product:` requirement it serves instead.

Nothing else goes in the record. How the code keeps the promise belongs in the spec, progress and tasks in the work
tracker, and why one option beat another in a decision.

## Engineering constraints (planning:engineering-constraints)

A constraint is a requirement nobody upstream asked for, so it has no "Serves" link. Typical ones are the language and
runtime ("The service is written in TypeScript"), data handling ("Member phone numbers never appear in logs"),
idempotency, delivery semantics, migration compatibility, observability targets, and things the system can't run
without, such as rotating TLS certificates before they expire. Engineering owns a constraint outright, so it is never an
assumption.

A constraint lives at the narrowest level it binds: the epic, the initiative when it spans several epics, the project
for the project's whole system, or the root for the whole program. Language, runtime, and program-wide data rules
usually sit at the root. If alternatives were weighed, a decision records why and the constraint cites it.

## Engineering sections (planning:engineering-sections)

An `engineering.md` holds, in order:

1. A `#` title, then one line citing the folder's `epic:` or `initiative:` id or naming its project. The root file has
   no such line.
2. Optionally, `## What already holds`: existing behaviour the work builds on, such as another epic's delivered
   requirement, a contract it consumes, or a system limit, each cited or linked, so the reader knows what not to rebuild
   or break.
3. The `engineering:` records.
4. Optionally, `## Open questions` (`planning:inline-questions`).

The root and project files hold only records that bind the whole program or project: constraints, and bounds derived
from the `product:` records at that same level.

## Removing a requirement (planning:requirement-removal)

A requirement that no longer binds is deleted, and the same change rewrites or removes every citation of its id
(`planning:change-in-place`). Nothing marks it as gone; if a decision drove the removal, that decision says why.
