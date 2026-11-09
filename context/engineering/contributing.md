# Contributing engineering content

## Engineering lifecycle (planning:lifecycle)

Engineering joins an epic's path at its third step, once product intent exists — a `product:` requirement, or wherever
the README declares product lives:

1. **Derive.** Write the requirements the product requirements need, an assumption where intent is missing, and the spec
   once the mechanics need their own readers, all in the epic's folder. Each cites the product intent it serves; product
   files never cite engineering ids back, so citation runs one way, from engineering to product.
2. **Slice.** Cut the epic into the ordered changes that build it, in its `slices/`
   ([workflows/slice-an-epic.md](./workflows/slice-an-epic.md)). Slicing often surfaces gaps; fill each at its home
   before a slice cites it (`planning:slice-lifecycle` in [slices.md](./slices.md)).
3. **File tracker work only once every prerequisite can be named** — a slice or epic it depends on, a requirement it
   builds on, an open decision it waits on. A filed slice records its tracker item in `external:`, and the tracker owns
   its progress from then on.
4. **Deliver and archive.** When the epic is delivered, its `status:` says so and its folder moves to `delivered/` and
   freezes (`planning:delivered-archive` in [layout.md](./layout.md)).

An epic moving into or out of an initiative changes every `engineering:`, `assume:`, and `decision:` scoped to it; the
change that moves it rewrites every full citation (`planning:moving-ids`).

## Commit messages (planning:commit-messages)

<!-- shared:commit-messages -->

Commits follow Conventional Commits, scoped by the epic or initiative id they touch —
`docs(reliable-borrowing/reservations): …` — or by the root file for a program-wide change. Use `feat` for a new
registry row or a new requirements, spec, or slice file, `chore` for a status move or an archive move, and `docs` for
any other edit. When a change moves work along its lifecycle, the body says which move — outline written, slices cut,
epic in progress, epic delivered and archived.

<!-- /shared:commit-messages -->

## Contribution checklists (planning:contributing)

Land every engineering change through the matching checklist below, then [Before finishing](#before-finishing). Each
step applies the rule it cites; the checklist keeps the records one change touches landing together.

### Adding a document

1. Pick the place by the reader's question and the layout — `planning:placement`, `planning:layout`.
2. Run the admission test — `planning:document-admission`. If the subject is already owned, improve the owner.
3. Give it the name and place the layout sets, or link it from the document owning its subject, in the same change —
   `planning:document-admission`. A new folder for an epic planned in a tracker gets its `epic.md`, pointing upstream —
   `planning:tracker-epic`.
4. Rewrite in place or delete what it overtakes — `planning:change-in-place`.

### Adding a requirement

1. Confirm it is engineering's to own — `planning:classify-requirement`. If a user could notice it changing, it belongs
   upstream or in an assumption; if it only describes how the code keeps a promise, it belongs in the spec.
2. Check it commits to something beyond the product requirement it serves; if it only restates one, write nothing —
   `planning:beyond-product`.
3. Find the epic it serves — `planning:capability-epics` — or, for a constraint serving no product requirement, the
   epic, initiative, or whole system it binds — `planning:engineering-constraints`.
4. Mint the id and add its section, headed by a short name and the bare id in parentheses, to that folder's
   `engineering.md`, or the root's — `planning:requirement-ids`, `planning:owned-scoped-ids`, `planning:id-citations`.
5. Write one or two sentences starting **Proposed.**, citing what it serves — `planning:requirement-record`,
   `planning:serves`. Add a README scheme row for any new scheme (`planning:scheme-declaration`); if the intent it needs
   is unstated, record an assumption first.
6. Add an `Acceptance:` list of bullets only engineering can verify, and put any product can judge under the product
   requirement instead — `planning:beyond-product`.

### Recording an assumption

1. Check upstream first; if any upstream id states the intent, serve it instead.
2. Check that it is product-shaped — `planning:assumption-record`, `planning:classify-requirement`. A technology
   constraint is an `engineering:` and a technology choice a `decision:`, never an assumption.
3. Mint the id and add its section, headed by a short name and the bare id in parentheses, to the folder's
   `assumptions.md`, stating in product terms what is assumed and why engineering had to.
4. Cite the assumption in each requirement that rests on it.

### Confirming or rejecting an assumption

1. Delete the record — `planning:assumption-lifecycle`.
2. If confirmed, move the intent to its product home in the same change and repoint every citation of the `assume:` id
   to it.
3. If rejected, re-derive or delete every requirement serving only it, and fix every other citation —
   `planning:rejected-assumption`, `planning:requirement-removal`.

### Recording a decision

1. Check it clears the bar — `planning:decision-bar`. A clarification edits the requirement or spec instead.
2. Choose the owner — `planning:decision-ownership` — and the slug — `planning:decision-slugs`; check the owner's
   `decisions.md` for a collision.
3. Write it in the owner's `decisions.md` — `planning:decision-format` — open if the call is deferred. A folder's first
   decision creates the file (`planning:decisions-file`).
4. When making an open decision or overturning a made one, rewrite its entry in place and keep the id.
5. Correct what it invalidates — delete requirements that no longer bind, rewrite specs in place or delete leaves
   (`planning:change-in-place`) — and cite the decision in each document it binds.

### Slicing an epic

Follow [workflows/slice-an-epic.md](./workflows/slice-an-epic.md) — `planning:slice-files`, `planning:slice-cuts`,
`planning:slice-order`, `planning:slice-lifecycle`.

### Reviewing requirements

Follow [workflows/requirements-review.md](./workflows/requirements-review.md) after product intent changes and before
slicing.

### Asking a clarifying question

Add a bullet to the `## Open questions` at the end of the file it concerns — `planning:inline-questions`. When it is
answered, fold the answer into the text and delete the bullet.

### Before finishing

- Every new document sits where the layout names it, or is linked from the document owning its subject.
- Every cited `engineering:`, `assume:`, and `decision:` is plain text and appears verbatim in a real heading or row — a
  bare one at the nearest level outward from the citing file that defines it — and each scheme id resolves through a row
  in the README's scheme table. No heading is an id alone.
- No citation points at a deleted id, and no scoped id changed except by moving its epic into or out of an initiative.
- Every slice still derives from what it cites, and every `depends-on` names a lower-numbered slice of its epic, or an
  epic or initiative.
- Nothing in `supporting/` was edited unless someone asked.
