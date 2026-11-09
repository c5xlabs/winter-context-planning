# Assumptions

When a requirement needs product intent that nobody has stated, engineering writes it down as an assumption and builds
on that, rather than quietly picking an answer inside a requirement or spec.

## Assumption records (planning:assumption-record)

An assumption lives in the `assumptions.md` of the folder whose requirements rest on it: one `##` record per assumption
under the file's `#` title, headed `<Name> (assume:<subject>)`. In folder form, each record is a leaf at
`assumptions/<subject>.md`.

A record is one or two sentences. It states the assumption the way product would — the person, their problem, what the
product promises them — and says why engineering had to assume it, citing the product requirement it fills a gap in when
that helps. Apart from that product framing it is written in the engineering voice (`planning:engineering-voice`). It
has no field list, index table, status word, or technology choice.

```markdown
## Cover length cap (assume:cover-max-duration)

A coordinator going away expects the hand-off to end on its own, so we assume the product promises cover lasts no more
than 30 days; `product:coordinator-cover` sets no bound, and expiry needs one.
```

An assumption is a made-up product requirement, so it has to pass the product test in `planning:classify-requirement`
([`../product/requirements.md`](../product/requirements.md)): a user could notice it changing, it is stated in user or
business terms, and any implementation could satisfy it. Technology and implementation choices ("the app is written in
C#", "uses a queue") are never assumptions; a constraint is an `engineering:` record and a choice between alternatives
is a decision. Product files never hold or cite an assumption.

## Assumption lifecycle (planning:assumption-lifecycle)

An assumption exists only while it is open. The change that settles it deletes the record, and either:

- **Confirmed** — product agreed, and the intent now lives in a product home, a product requirement, an epic, or a
  tracker item. The same change repoints every citation of the `assume:` id to the id now holding the intent.
- **Rejected** — product refused it. The same change handles the requirements resting on it, as below, and rewrites or
  removes every other citation of the `assume:` id.

## Rejected assumptions (planning:rejected-assumption)

When an assumption is rejected, every requirement that served only it is re-derived from what product said instead, or
deleted (`planning:requirement-removal`). No requirement is left serving a deleted assumption.
