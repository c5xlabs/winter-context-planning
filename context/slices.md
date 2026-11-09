# Slices

How an epic is cut into the changes that build it. To cut an epic's slices, follow
[`./workflows/slice-an-epic.md`](./workflows/slice-an-epic.md).

## Slice files (planning:slice-files)

A slice is one mergeable change toward the epic's requirements and spec, small enough to file as one work-tracker item.
Each lives in the epic's `slices/` folder as `<nn>-<name>.md`, where `nn` is its two-digit build order from `01` and
`name` names the change rather than the outcome (`01-hold-store.md`). The folder has no index.

```yaml
---
name: hold-at-confirmation         # required; matches the filename after its number
external: jira:SHED-62             # optional; the tracker item, one <system>:<id>, once it has one
depends-on:                        # optional; what must land first
  - hold-store                     # a slice of this epic, by name
  - epic:reliable-borrowing/reservations  # or an epic or initiative, by id
code:                              # optional; where the behaviour it changes lives today
  - toolshed-api/src/reservations/book.ts::bookWindow
---
```

`code:` entries are `<repo>/<path>::<symbol>`, pointing at a function, class, or type rather than a line. A slice that
only adds code nothing calls yet leaves `code:` out.

The body follows, in order:

1. A `#` title and one short paragraph: what the change builds, the `product:` and `engineering:` requirements and spec
   sections it delivers, the constraint or decision that shapes it, and any open decision it waits on.
2. `## Change` — a short list of what the system does once it lands that it did not before, and what it leaves alone.
3. `## Acceptance` — the checks that show it is done, each verifiable by a test.
4. Optionally, `## Out of scope` — neighbouring work a reader might expect here, naming the slice or epic that has it.

Apart from its `code:` pointers, a slice holds nothing of its own. Every fact in it comes from the epic's requirements,
assumptions, spec, or decisions, or from a constraint binding the epic, and the slice cites it there. If a slice needs a
fact none of them states, add the fact to its home first. Slices can then always be deleted and cut again without loss.

Nothing outside an epic's `slices/` names one of its slices. Slices carry no status: the tracker owns their progress,
and the epic's `status:` says when the whole epic is delivered. They are written in the engineering voice
(`planning:engineering-voice` in [`./voice.md`](./voice.md)).

## Cutting slices (planning:slice-cuts)

Cut by mechanism and surface, not by what a user notices. Each slice is a change a reviewer can hold in their head,
merges on its own with its tests passing, and leaves the main branch releasable. The usual sequence:

1. **The seam or record** — the table, interface, or contract the rest stands on, with nothing calling it yet.
2. **Each surface in turn** — an API, a worker, an event consumer, a screen — building on the seam.
3. **Carry-over** — migrating or backfilling existing data, when there is any.
4. **Proof** — an end-to-end slice, when no surface slice exercises the whole path.
5. **The harness** — the procedure or guide people need once the change is theirs.

The constraints binding the epic, at every level from the epic up to the root, decide how a change reaches a system
already in use. Each strategy is its own run of slices:

| Strategy              | When                                                   | Slices, in order                                                                  |
| --------------------- | ------------------------------------------------------ | --------------------------------------------------------------------------------- |
| Expand and contract   | A contract others call must stay backward compatible   | Add the new shape → move every caller → deprecate the old → retire it             |
| Feature flag          | Unfinished behaviour must not reach people who use it  | Build behind a flag that is off → turn it on → remove the flag and its off path   |
| Branch by abstraction | A mechanism in use is replaced while work keeps moving | Put a seam around the old one → build the new one behind it → switch → remove old |

The closing step — retiring, removing the flag, removing the old mechanism — is always a slice of its own. If no
constraint settles the strategy and the choice matters, record it as a decision before cutting (`planning:decision-bar`
in [`./decisions.md`](./decisions.md)).

Every requirement in the epic, and every acceptance bullet under it, is delivered by at least one slice, and every spec
section is built by one. A requirement no slice delivers is either unplanned work or shouldn't be there. A slice that
needs a design of its own means the spec is missing a section: write it and cite it.

## Slice order (planning:slice-order)

The numbers give the build order and `depends-on` gives the reasons. Every slice a slice depends on has a lower number;
slices with no dependency between them can be built in parallel.

A slice depends on another only when it builds on something that one introduces — a table, an interface, an event, a
flag. Touching the same file is not a dependency; the later slice rebases. If a slice can be built against a mock and
the interface it needs is already settled, it depends on the slice that lands the interface, not the one implementing
it.

A slice never depends on another epic's slice. When it needs part of another epic, it depends on that epic or its
initiative by id.

## Slice lifecycle (planning:slice-lifecycle)

An epic can be sliced at any time. Slicing works best once requirements are settled and the spec is complete, but
slicing early is a good way to find gaps: each missing fact becomes an assumption, requirement, decision, spec section,
or open question.

Re-slicing rewrites `slices/` in place. A slice with an `external:` keeps its name and `external:` as long as it
describes the same change; the rest can be renumbered, rewritten, or deleted. The folder moves to `delivered/` with its
epic and freezes there (`planning:delivered-archive` in [`./layout.md`](./layout.md)).
