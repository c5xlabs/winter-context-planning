# Product requirements

The product requirements in an epic's `requirements.md`, or inline in its `epic.md`: what makes a statement product's to
require, the shape of a requirement record, its acceptance bullets, and how records spread into their own files. The
files fronting a work folder are [`./intent.md`](./intent.md).

## Classifying a requirement (preq:classify-requirement)

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

## Requirement records (preq:requirement-records)

A product requirement is a record of its own, named for what it requires. Whatever supports a requirement — an
engineering requirement serving it, a decision, a tracker item — may cite its id, and that citation is the only link. An
epic's `requirements.md` holds, in order:

1. A `#` title, then one line citing the epic's `epic:` id.
2. One record per requirement: a `## <Name> (product:<subject>)` heading, the name a short phrase for the capability and
   the subject naming what it requires (`preq:id-citations` in [`./namespaces.md`](./namespaces.md)); then one or two
   plain sentences of what changes for the person once it holds, linking any mockup and citing any `decision:` inline;
   then its acceptance bullets. A requirement no longer wanted is deleted, and every citation of it rewritten or removed
   in the same change (`preq:change-in-place` in [`./structure.md`](./structure.md)).
3. Optional: `## Open questions`.

<!-- shared:requirement-status -->

A requirement has one optional status, the **Proposed.** marker opening its body: written down but not yet binding. A
requirement without it is accepted and binds; build and test to it. The change that accepts a proposed requirement drops
the marker. Proposed and accepted are the only two states, and nothing records whether a requirement is met.

<!-- /shared:requirement-status -->

Never: prose between records, the problem restated, status, slices, stories, test-level criteria, or engineering ids.

A small epic may skip the file and write the same records inline in `epic.md`, after its intent, under a
`## Requirements` heading, each record a `###` section, the same pattern as file-or-folder (`preq:file-or-folder`): a
record keeps its name, id, and shape in either file, so moving it changes only its heading level. An epic planned in a
tracker has no records here.

```markdown
## Coordinator cover (product:coordinator-cover)

A coordinator going away hands their calls on the catalog and the roster to a shift volunteer for a set time, and the
calls return to them when the time is up.

Acceptance:

- A volunteer with a question for the coordinator sees who is covering.
- The calls return to the coordinator when the cover ends.
```

An initiative's `requirements.md` takes the same shape, its opening line citing the `initiative:` id, and each record
takes a subject no epic in the initiative has as its slug, so a full id never reads as an epic.

## Requirement acceptance (preq:requirement-acceptance)

A requirement record may close with a short `Acceptance:` list — a few bullets of what product judges at acceptance by
watching the outcome: what the person is told, what they see, what they can do, and how soon. Each bullet is observable
without knowing how the system works (`preq:classify-requirement`); a bound engineering derives to keep it, or how the
code keeps it, belongs to engineering instead.

## Requirement files (preq:requirement-files)

When an epic's requirement records outgrow one file, move to the folder form, one leaf per requirement and no index —
`requirements/<subject>.md` (`preq:file-or-folder` in [`./layout.md`](./layout.md)). The epic frontmatter names no leaf.
A leaf holds its record under the same heading and may carry frontmatter naming its epic, never a status, a slice, or an
`external:` value:

```yaml
---
epic: volunteer-shifts
---
```
