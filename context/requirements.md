# Product requirements

An epic's product requirements live in its `requirements.md`, or inline in its `epic.md`. The files that front a work
folder are covered in [`./intent.md`](./intent.md).

## Classifying a requirement (planning:classify-requirement)

To find a statement's home, ask three questions in order. Could a user notice it changing? Then it is a product
requirement (`product:`), or an assumption (`assume:`) if product never said it. Does it only describe how the code
keeps a promise? Then it belongs in the spec. Does it bind every implementation? Then it is an engineering requirement
(`engineering:`): either a bound derived from a product promise, which engineering may change alone while the promise
holds, or a standalone constraint nobody upstream asked for, such as the runtime, data handling, idempotency, delivery
semantics, migration compatibility, or tracing. A choice between real alternatives is also recorded as a `decision:`
with its reason, wherever its outcome lands.

One topic, traced through every home:

| Statement                                                                                                              | Home           |
| ---------------------------------------------------------------------------------------------------------------------- | -------------- |
| A volunteer cannot check in a tool they borrowed themselves.                                                           | `product:`     |
| A member hears their reservation lapsed within five minutes of the shift closing.                                      | `product:`     |
| (Product never gave a time.) A member needs to hear their reservation lapsed within five minutes of the shift closing. | `assume:`      |
| The `reservation.lapsed` event is consumed within 10 s at p95.                                                         | `engineering:` |
| `CHECK (checked_in_by <> borrower_id)`                                                                                 | spec, `Data`   |
| Loan periods kept in a table rather than in code, because the coordinator sets one per tool category.                  | `decision:`    |

Some statements only sound like requirements. "Use a transaction around the check" is spec. "It should be fast" is a
promise with no number, so it becomes an open `decision:` or an `assume:`.

## Requirement records (planning:requirement-records)

Each product requirement is its own record, named for what it requires. Anything that supports it, whether an
engineering requirement, a decision, or a tracker item, may cite its id, and that citation is the only link between
them.

An epic's `requirements.md` opens with a `#` title and one line citing the epic's `epic:` id, then has one record per
requirement, then optionally `## Open questions`. A record is a `## <Name> (product:<subject>)` heading, where the name
is a short phrase for the capability and the subject names what it requires (see `planning:id-citations`); then one or
two plain sentences on what changes for the person once it holds, linking any mockup and citing any `decision:` inline;
then its acceptance bullets. Nothing else goes in the file: no prose between records, no restated problem, and no
status, slices, stories, test-level criteria, or engineering ids.

```markdown
## Coordinator cover (product:coordinator-cover)

A coordinator going away hands their calls on the catalog and the roster to a shift volunteer for a set time, and the
calls return to them when the time is up.

Acceptance:

- A volunteer with a question for the coordinator sees who is covering.
- The calls return to the coordinator when the cover ends.
```

A requirement is accepted and binding unless its body opens with **Proposed.**, which means written down but not yet
binding. Accepting it drops the marker. There are no other states, and nothing records whether a requirement is met. A
requirement no longer wanted is deleted, and every citation of it is rewritten or removed in the same change (see
`planning:change-in-place`).

A small epic may skip the file and put the same records in `epic.md` under a `## Requirements` heading after its intent,
each record a `###` section. Moving a record between the two changes only its heading level. An epic planned in a
tracker has no records here.

Initiatives, projects, and the program at the root may have a `requirements.md` of the same shape. An initiative's
opening line cites its `initiative:` id, a project's names the project, and the program's has none. These hold only
requirements that bind every epic beneath them; a program requirement is a promise every epic keeps, such as a format
every surface emits, not direction the charter already gives. Each record's subject must differ from every initiative
and epic slug beneath it, so its id never reads as an epic's.

## Requirement acceptance (planning:requirement-acceptance)

A record may close with a short `Acceptance:` list: a few bullets product can judge by watching the outcome, covering
what the person is told, what they see, what they can do, and how soon. Each bullet must be observable without knowing
how the system works. A derived bound, or how the code meets the bullet, belongs to engineering.

## Requirement files (planning:requirement-files)

When an epic's records outgrow one file, switch to a folder with one leaf per requirement, `requirements/<subject>.md`,
and no index (see `planning:file-or-folder`). The epic frontmatter names no leaf. A leaf keeps its record's heading and
may carry frontmatter naming its epic, but never a status, a slice, or an `external:` value:

```yaml
---
epic: volunteer-shifts
---
```
