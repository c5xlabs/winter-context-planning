# Slices

How an epic is cut into the changes that build it: what a slice file holds, how the cuts are made, how they are ordered,
and how slices change. To cut an epic's slices, follow [workflows/slice-an-epic.md](./workflows/slice-an-epic.md).

## Slice files (planning:slice-files)

A slice is one mergeable change toward the epic's requirements and spec, written so it can be filed as one work-tracker
item. An epic's slices live in its `slices/` folder, one file each, named `<nn>-<name>.md`: `nn` is the build order, two
digits from `01`, and `name` is a slug naming the change, not the outcome (`01-hold-store.md`). The folder has no file
form and no index. Each file opens with frontmatter:

```yaml
---
name: hold-at-confirmation         # required; matches the filename after its number
external: jira:SHED-62             # optional; the slice's tracker item, one <system>:<id>, once it has one
depends-on:                        # optional; what must land first
  - hold-store                     # a slice of this epic, by name
  - epic:reliable-borrowing/reservations  # or an epic or initiative, by id
code:                              # optional; where the behaviour it changes lives today
  - toolshed-api/src/reservations/book.ts::bookWindow
---
```

`code:` points at the code the slice changes as it stands today, one `<repo>/<path>::<symbol>` entry each: the
repository's name, the file's path from its root, and the function, class, or type, since a symbol survives edits that
shift line numbers. A slice that only adds new code with nothing calling it leaves `code:` out.

Then, in order:

1. A `#` title, then one short paragraph saying what the change builds, citing the `product:` and `engineering:`
   requirements and the spec sections it delivers, the constraint or decision that shapes it, and any open decision it
   waits on.
2. `## Change` — the change as a short list: what the system does once it lands that it did not before, and what it
   leaves alone.
3. `## Acceptance` — the checks that show this change is done, each verifiable by a test.
4. Optional: `## Out of scope` — neighbouring work a reader might expect here, naming the slice or epic that has it.

A slice derives; beyond its `code:` pointers, it holds nothing of its own. Every fact in it is stated by the epic's
requirements, assumptions, spec, or decisions, or by a constraint binding the epic, and the slice cites it. When cutting
a slice needs a fact no such file holds, that fact goes to its home first and the slice cites it there. So the slices
can be deleted and cut again from the same sources, and their pointers found again in the code, without losing anything.
For the same reason nothing outside its own `slices/` names a slice: no requirement, spec, decision, or other epic's
slice cites one. Slices carry no status; the work tracker owns their progress, and the epic's own `status:` says when
the whole epic is delivered. Slices are written in the engineering voice (`planning:engineering-voice` in
[voice.md](./voice.md)).

## Cutting slices (planning:slice-cuts)

Cut by mechanism and surface, never by what a user notices. A slice is one change a reviewer can hold in their head: it
merges on its own, its tests pass, and the main branch stays releasable after it. The usual sequence:

1. **The seam or record first** — the table, interface, or contract the rest stands on, with nothing calling it yet.
2. **Each surface in turn** — an API, a worker, an event consumer, a screen — each building on the seam.
3. **Carry-over** — migrating or backfilling what exists, when anything does.
4. **Proof** — an end-to-end slice, when no surface slice exercises the whole path.
5. **The harness** — the procedure or guide people need once the change is theirs.

The constraints binding the epic — in its `engineering.md`, its initiative's, and the root's — choose how a change
reaches a system already in use, and each strategy is a sequence of slices of its own:

| Strategy              | When                                                   | Slices, in order                                                                  |
| --------------------- | ------------------------------------------------------ | --------------------------------------------------------------------------------- |
| Expand and contract   | A contract others call must stay backward compatible   | Add the new shape → move every caller → deprecate the old → retire it             |
| Feature flag          | Unfinished behaviour must not reach people who use it  | Build behind a flag that is off → turn it on → remove the flag and its off path   |
| Branch by abstraction | A mechanism in use is replaced while work keeps moving | Put a seam around the old one → build the new one behind it → switch → remove old |

The closing step of a strategy — retiring, removing the flag, removing the old mechanism — is always a slice, never a
note on another, so the cleanup is planned and tracked like the rest. When no constraint settles the strategy and the
choice matters, record it as a decision before cutting (`planning:decision-bar` in [decisions.md](./decisions.md)).

Every `product:` and `engineering:` requirement the epic holds, and every acceptance bullet under it, is delivered by at
least one slice, and every spec section is built by one; a requirement no slice delivers is unplanned work or a
requirement that should not be there. A slice that needs a design of its own means the spec is missing a section, so
write the section and cite it.

## Slice order (planning:slice-order)

The numbers are the order the slices are built in, and `depends-on` says why. A slice depends on another only when it
builds on something that one introduces — a table, an interface, an event, a flag — never because both change the same
file: a dependency orders building, not merging, and the later of two slices touching one file rebases. When a slice can
be built against a mock of what it builds on, and the interface it needs is already established, it depends only on the
slice that lands that interface, not on the one implementing it. A slice depends on a slice of its own epic by name, or
on another epic or initiative by its `epic:` or `initiative:` id, never on another epic's slice: when it needs part of
another epic, it depends on that epic, and the other epic's slices are that epic's to order. Every slice a slice depends
on has a lower number, so the numbering is always a valid build order. Slices with no dependency between them can be
built in parallel; the numbers commit only to one order that works.

## Slice lifecycle (planning:slice-lifecycle)

An epic can be sliced at any time. The cut is best once its requirements are settled and its spec is complete, but
slicing earlier is how gaps surface: a fact a slice needs and no file states becomes an assumption, a requirement, a
decision, a spec section, or an open question, and the epic is better for it. Re-slicing rewrites `slices/` in place: a
slice with an `external:` keeps its name and `external:` while it still describes the same change, and the rest are
renumbered, rewritten, or deleted freely. The folder moves to `delivered/` with its epic (`planning:delivered-archive`
in [layout.md](./layout.md)) and freezes there, like the spec.
