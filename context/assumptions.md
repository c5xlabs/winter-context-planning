# Assumptions

Assumption records in a work folder's `assumptions.md`: product intent engineering writes down and answers for because
no one has stated it yet.

## Assumption records (planning:assumption-record)

When a requirement needs product intent that does not exist, write an assumption and serve it; never pick the answer
silently inside a requirement or spec. The `assumptions.md` in the folder whose requirements rest on it holds a `#`
title, then one `##` record per assumption, headed `<Name> (assume:<subject>)` (`planning:id-citations`): one or two
sentences stating the assumption as product would — the person, their problem, what the product promises them — and why
engineering had to assume it, citing the product requirement it fills a gap in where the prose needs it. Never: a field
list or index table, a status word, or a technology choice. In folder form (`planning:file-or-folder`), each leaf is
`assumptions/<subject>.md`. Beyond stating the assumption in product terms, the record is written in the engineering
voice (`planning:engineering-voice` in [`./voice.md`](./voice.md)).

```markdown
## Cover length cap (assume:cover-max-duration)

A coordinator going away expects the hand-off to end on its own, so we assume the product promises cover lasts no more
than 30 days; `product:coordinator-cover` sets no bound, and expiry needs one.
```

An assumption must be product-shaped: a made-up product requirement that passes the first tell of
`planning:classify-requirement` in [`./engineering.md`](./engineering.md). A user could notice it changing, it is stated
in user or business terms, and any implementation could satisfy it. Technology and implementation choices ("the app is
written in C#", "data is stored in git", "uses a queue") are never assumptions: a constraint is an `engineering:` record
(`planning:engineering-constraints`), and a choice between alternatives is a decision. An assumption never lives in a
product file, and no product file cites it.

## Assumption lifecycle (planning:assumption-lifecycle)

An assumption exists only while it is open, so its record carries no status word. The change that settles it deletes the
record (`planning:change-in-place` in [`./structure.md`](./structure.md)):

- Confirmed — product agreed, and the intent moved to a product home, a product requirement, an epic, or a tracker item.
  The same change repoints every citation of the `assume:` id to the id now holding the intent.
- Rejected — product refused it. The same change re-derives or deletes every requirement resting only on it
  (`planning:rejected-assumption`), and rewrites or removes every other citation of the `assume:` id.

## Rejected assumptions (planning:rejected-assumption)

When an assumption is rejected, in the same change re-derive every requirement that serves only it from what product
said instead, or delete it (`planning:requirement-removal` in [`./engineering.md`](./engineering.md)). No requirement
may be left serving a deleted assumption.
