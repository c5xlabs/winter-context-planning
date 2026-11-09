# Engineering requirements

Engineering requirements in a work folder's `engineering.md`: one record per `engineering:` id, each stating what
engineering commits to.

## Classifying a requirement (ereq:classify-requirement)

<!-- shared:classify-requirement -->

Three tells, asked in order, give any statement about the system its home. Could a user notice it changing? Then it is a
product requirement (`product:`), or an assumption (`assume:`) when product never said it. Does it only describe how the
code keeps a promise? Then it belongs in the spec, not in any requirement. Otherwise, does it bind every implementation?
Then it is an engineering requirement (`engineering:`), in one of two shapes: a bound derived from a product promise,
which engineering can change alone so long as the promise holds, or a standalone constraint nobody upstream asked for —
the language and runtime, data handling, idempotency, delivery semantics, migration compatibility, tracing. A choice
between real alternatives is a decision recording its reason, whichever home its outcome takes. One topic, traced
through every home:

| Statement                                                                                                              | Home           | Why                                                                                    |
| ---------------------------------------------------------------------------------------------------------------------- | -------------- | -------------------------------------------------------------------------------------- |
| A volunteer cannot check in a tool they borrowed themselves.                                                           | `product:`     | A coordinator would notice if it broke.                                                |
| A member hears their reservation lapsed within five minutes of the shift closing.                                      | `product:`     | A member would notice an hour; changing it is a product call.                          |
| (Product never gave a time.) A member needs to hear their reservation lapsed within five minutes of the shift closing. | `assume:`      | Product-shaped, made up by engineering, held until product confirms.                   |
| The `reservation.lapsed` event is consumed within 10 s at p95.                                                         | `engineering:` | A bound engineering derived so the five minutes hold; engineering can change it alone. |
| `CHECK (checked_in_by <> borrower_id)`                                                                                 | spec, `Data`   | How the code keeps the no-self-check-in promise.                                       |
| Loan periods kept in a table rather than in code, because the coordinator sets one per tool category.                  | `decision:`    | A choice between real alternatives, with its reason.                                   |

Two statements that sound like requirements are neither. "Use a transaction around the check" is spec. "It should be
fast" is a product promise with no number, so it becomes an open `decision:` or an `assume:`.

<!-- /shared:classify-requirement -->

## Requirement ids (ereq:requirement-ids)

A requirement's id is `engineering:<owner id>/<subject>`, the owner being the epic or initiative whose folder holds it,
or `engineering:<subject>` for one the root holds; a bare id resolves outward from the citing folder (`ereq:bare-ids`),
and a move into or out of an initiative rewrites full ids (`ereq:moving-ids`). So
`engineering:overdue-returns/overdue-sweep` in `work/overdue-returns/` becomes
`engineering:reliable-borrowing/overdue-returns/overdue-sweep` if the epic moves under `reliable-borrowing`, and that
move rewrites every full citation, while `engineering:overdue-sweep` inside the folder stays. Otherwise an id is never
renamed or reused. A record moves only with its whole folder — into `delivered/`, keeping its id; one that belongs to
another epic is deleted here and minted under a new id there, in a change that rewrites every citation
(`ereq:requirement-removal`).

## Requirement records (ereq:requirement-record)

Every requirement is a `##` section headed `<Name> (engineering:<subject>)` (`ereq:id-citations`), then one or two
sentences of what engineering commits to: a bound derived from a product promise, citing inline the intent it serves
(`ereq:serves` in [derivation.md](./derivation.md)), or a standalone constraint (`ereq:engineering-constraints`). There
are no fields and no "implemented" state: delivery lives in the work tracker and the upstream intent. In folder form
(`ereq:file-or-folder`), each leaf is `engineering/<subject>.md`, with no index. The record carries the behaviour and
its reason in prose, which the spec leaves out (`ereq:spec-contracts` in [specs.md](./specs.md)). Records are written in
the engineering voice (`ereq:engineering-voice` in [voice.md](./voice.md)).

<!-- shared:requirement-status -->

A requirement has one optional status, the **Proposed.** marker opening its body: written down but not yet binding. A
requirement without it is accepted and binds; build and test to it. The change that accepts a proposed requirement drops
the marker. Proposed and accepted are the only two states, and nothing records whether a requirement is met.

<!-- /shared:requirement-status -->

```markdown
## Cover expiry (engineering:cover-expiry)

A stand-in's coordinator calls are refused within 60 seconds of the cover's end time, so the calls are back with the
coordinator when the product promises. Serves `product:coordinator-cover`.

Acceptance:

- A roster change the stand-in submits 61 seconds after the end time is refused.
```

## Beyond product (ereq:beyond-product)

A requirement never restates a product requirement: it states what engineering commits to beyond it, or it is not
written. Acceptance criteria are optional — an `Acceptance:` list of at most a few bullets under the sentences, as on a
product requirement, each one engineering can verify by a test or a measurement, with no word a test cannot check
("should", "fast", "user-friendly"). A criterion a user could notice, such as what the member is told, what the
volunteer sees, or how soon, is an acceptance bullet under the `product:` requirement it serves, in `requirements.md` or
the epic's `epic.md`. Nothing else goes in the record: how the code keeps a promise belongs in the spec, progress and
task breakdown in the work tracker, and why one option beat another in a decision.

## Engineering constraints (ereq:engineering-constraints)

A standalone constraint, one nobody upstream asked for — the language and runtime ("The service is written in
TypeScript"), data handling ("Member phone numbers never appear in logs"), idempotency, delivery semantics, migration
compatibility, tracing, metrics, alerts, and logging targets, or a necessity the system cannot run without, such as
rotating TLS certificates before expiry — is an `engineering:` record that stands without a "Serves" link. It lives at
the narrowest level it binds: the `engineering.md` of the epic whose work it binds, of the initiative when it binds
several of its epics, or of the root when it binds the whole system, as the language, the runtime, or a rule for
handling one kind of data everywhere usually does. When alternatives were weighed, a decision records why, and the
record cites it. It is never an assumption: engineering owns it outright.

## Engineering sections (ereq:engineering-sections)

A `engineering.md` holds, in order:

1. A `#` title, then one line citing the folder's `epic:` or `initiative:` id; the root file omits the line.
2. Optional: `## What already holds` — behaviour the work builds on that exists already, such as another epic's
   delivered requirement, a contract it consumes, or a system limit, each cited by id or linked, so a reader knows what
   not to rebuild and what not to break.
3. The `engineering:` records (`ereq:requirement-record`), any of them opening **Proposed.**
4. Optional: `## Open questions` (`ereq:inline-questions` in [decisions.md](./decisions.md)).

The root file holds only constraints binding the whole system (`ereq:engineering-constraints`). Never: restated product
text, progress, or tasks.

## Removing a requirement (ereq:requirement-removal)

A requirement that no longer binds is deleted, and the same change rewrites or removes every citation of its id
(`ereq:change-in-place` in [structure.md](./structure.md)). Nothing marks it as gone; a decision behind the removal says
why.
