# Contributing requirements content

## Epic lifecycle (planning:lifecycle)

Every epic takes the same path from idea to delivered, and each step is a deliberate change rather than a drift:

1. **Row and epic together.** The epic's row in `epics.md` and its `epic.md` land in the same change, the file at
   `refinement: outline` with its frontmatter and at least one sentence of the problem (`planning:epic-registry`,
   `planning:epic-frontmatter`); an epic is never named without its file. A milestone demanding it enters first or with
   it.
2. **Deepen as the work gets close.** When work is weeks away, `epic.md` grows its outcome and `## Left for later`, and
   `requirements.md` its requirements and their acceptance bullets (`planning:requirement-records`); open calls become
   open decisions (`planning:decision-format`). The product owner re-grades refinement; an agent never chooses a grade
   and writes `outline` on anything it creates.
3. **Engineering derives.** Engineering writes its requirements, any assumptions, and the spec in the same folder, each
   citing the product requirement it serves. Product files never cite them back (`planning:product-cites-product`);
   engineering's own steps are `planning:engineering-lifecycle`.
4. **File tracker work only once every prerequisite can be named** — landed already, or filed beside it. Engineering
   cuts the epic into the tracker items that build it. When work on the epic starts, its frontmatter moves to
   `status: in-progress`, and the same change sets its cell in every milestone chart naming it (`planning:epic-status`,
   `planning:milestone-registry`).
5. **Deliver and archive.** Evidence of delivery sets `status: delivered`, and that one change archives the epic and
   updates every registry naming it, following [`./workflows/deliver-an-epic.md`](./workflows/deliver-an-epic.md).

Turning an epic into an initiative, moving an epic into or out of one, or moving either to another project, is a
deliberate change of its own: it changes the epic's id and every `product:`, `engineering:`, `assume:`, and `decision:`
id scoped to it, and that change rewrites every citation in the repo (`planning:moving-ids`).

## Engineering lifecycle (planning:engineering-lifecycle)

Engineering joins an epic's path at its third step (`planning:lifecycle`), once product intent exists — a `product:`
requirement, or wherever the README declares product lives:

1. **Derive.** Write the requirements the product requirements need, an assumption where intent is missing, and the spec
   once the mechanics need their own readers, all in the epic's folder. Each cites the product intent it serves; product
   files never cite engineering ids back, so citation runs one way, from engineering to product.
2. **Slice.** Cut the epic into the ordered changes that build it, in its `slices/`
   ([`./workflows/slice-an-epic.md`](./workflows/slice-an-epic.md)). Slicing often surfaces gaps; fill each at its home
   before a slice cites it (`planning:slice-lifecycle` in [`./slices.md`](./slices.md)).
3. **File tracker work only once every prerequisite can be named** — a slice or epic it depends on, a requirement it
   builds on, an open decision it waits on. A filed slice records its tracker item in `external:`, and the tracker owns
   its progress from then on.
4. **Deliver and archive.** When the epic is delivered, its `status:` says so and its folder moves to `delivered/` and
   freezes (`planning:delivered-archive` in [`./layout.md`](./layout.md)).

## Commit messages (planning:commit-messages)

Commits follow Conventional Commits, scoped by the epic or initiative id they touch —
`docs(reliable-borrowing/reservations): …`, carrying its project in a repo with projects, `docs(fleet/board): …` — or by
the project for a project-wide change, and by the root file for a program-wide one. Use `feat` for a new registry row or
a new requirements, spec, or slice file, `chore` for a status move or an archive move, and `docs` for any other edit.
When a change moves work along its lifecycle, the body says which move — outline written, slices cut, epic in progress,
epic delivered and archived.

## Contribution checklists (planning:contributing)

Land every change through the matching checklist below, then [Before finishing](#before-finishing). Each step applies
the rule it cites; the checklist keeps the records one change touches — a decision, the decision it overturns, the
documents it corrects — landing together.

### Adding a document

1. Pick the place by the reader's question and the layout — `planning:placement`, `planning:layout`.
2. Run the admission test — `planning:document-admission`. If the subject is already owned, improve the owner.
3. Cite every id as plain text, and give every record it defines a `<Name> (<id>)` heading — `planning:id-citations`.
4. Give it the name and place the layout sets, or link it from the document owning its subject, in the same change —
   `planning:document-admission`. A new epic or initiative folder gets its `epic.md` or `initiative.md` and its registry
   row together; in a repo holding no product content, a new folder for an epic planned in a tracker gets its `epic.md`,
   pointing upstream — `planning:tracker-epic`.
5. Rewrite in place or delete what it overtakes — `planning:change-in-place`.

### Adding an engineering requirement

1. Confirm it is engineering's to own — `planning:classify-requirement`. If a user could notice it changing, it belongs
   upstream or in an assumption; if it only describes how the code keeps a promise, it belongs in the spec.
2. Check it commits to something beyond the product requirement it serves; if it only restates one, write nothing —
   `planning:beyond-product`.
3. Find the epic it serves — `planning:capability-epics` — or, for a constraint serving no product requirement, the
   epic, initiative, project, or whole program it binds — `planning:engineering-constraints`.
4. Mint the id and add its section, headed by a short name and the bare id in parentheses, to that folder's
   `engineering.md`, or the project's or root's — `planning:requirement-ids`, `planning:owned-scoped-ids`,
   `planning:id-citations`.
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
2. Choose the owner — `planning:decision-ownership` — which fixes the file and the id's scope; then the slug —
   `planning:decision-slugs` — checking the owner's `decisions.md`, and every level outward, for a collision.
3. Write it in the owner's `decisions.md` — `planning:decision-format` — open if the call is deferred. A folder's first
   decision creates the file (`planning:decisions-file`).
4. When making an open decision or overturning a made one, rewrite its entry in place and keep the id.
5. Rewrite what it invalidates in place, or delete it — a requirement that no longer binds, a spec leaf — fixing every
   citation of a deleted id (`planning:change-in-place`); cite the decision in each document it binds.

### Slicing an epic

Follow [`./workflows/slice-an-epic.md`](./workflows/slice-an-epic.md) — `planning:slice-files`, `planning:slice-cuts`,
`planning:slice-order`, `planning:slice-lifecycle`.

### Reviewing requirements

Follow [`./workflows/requirements-review.md`](./workflows/requirements-review.md) after product intent changes and
before slicing.

### Asking a clarifying question

Add a bullet to the `## Open questions` at the end of the file it concerns — `planning:inline-questions`. When it is
answered, fold the answer into the text and delete the bullet.

### Before finishing

- Every new document sits where the layout names it, or is linked from the document owning its subject.
- Every cited id is plain text and appears verbatim in a real row, heading, or frontmatter field — a bare one at the
  nearest level outward from the citing file that defines it — and each scheme id resolves through a row in the README's
  scheme table. No heading is an id alone.
- No citation points at a deleted id, and no scoped id changed except by moving its epic into or out of an initiative,
  or to another project.
- No subject is defined at two levels on one path to the root (`planning:no-shadowing`), and no initiative, epic, or
  program record takes a project's slug (`planning:project-slugs`).
- No product-owned file cites an `engineering:` or `assume:` id or links an engineering file
  (`planning:product-cites-product`).
- Every changed `epic.md` or `initiative.md` still satisfies its frontmatter rule, every milestone chart naming a
  changed epic shows its status (`planning:milestone-registry`), and every newly reached milestone has moved to
  `delivered.md` (`planning:delivery-ledger`).
- An epic whose `status:` is `delivered` sits in `delivered/`; any other epic stays in `work/`.
- Every slice still derives from what it cites, and every `depends-on` names a lower-numbered slice of its epic, or an
  epic or initiative.
- Nothing in `supporting/` was edited unless someone asked.
