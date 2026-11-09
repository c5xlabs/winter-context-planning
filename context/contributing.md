# Contributing requirements content

## Epic lifecycle (planning:lifecycle)

Every epic takes the same path from idea to delivered, and each step is a deliberate change:

1. **Name it with its file.** The epic's `epic.md` lands in the change that names the epic, at
   `refinement: outline`, with its frontmatter and at least a sentence of the problem. A milestone that demands the epic
   lands first or with it.
2. **Deepen as the work gets close.** When the work is weeks away, `epic.md` gains its outcome and `## Left for later`,
   and `requirements.md` its requirements with their acceptance bullets. Open calls become open decisions. Only the
   product owner grades refinement; an agent writes `outline` on anything it creates and never changes the grade.
3. **Engineering derives** its requirements, assumptions, and spec in the same folder, following the engineering
   lifecycle below.
4. **File tracker work once every prerequisite can be named**, as already landed or filed alongside. When work starts,
   the epic moves to `status: in-progress`, and the same change updates its cell in every milestone chart that names it.
5. **Deliver and archive** through [`./workflows/deliver-an-epic.md`](./workflows/deliver-an-epic.md).

Turning an epic into an initiative, moving an epic into or out of one, or moving either to another project changes the
epic's id and every `product:`, `engineering:`, `assume:`, and `decision:` id scoped to it. That change rewrites every
citation in the repo (`planning:moving-ids`).

## Engineering lifecycle (planning:engineering-lifecycle)

Engineering starts once product intent exists, as a `product:` requirement or wherever the README says product lives.

1. **Derive.** In the epic's folder, write the requirements the product needs, an assumption wherever intent is missing,
   and the spec once the mechanics need their own readers. Each cites the product intent it serves. Citation runs one
   way: product files never cite engineering ids.
2. **Slice.** Cut the epic into the ordered changes that build it, in its `slices/`, following
   [`./workflows/slice-an-epic.md`](./workflows/slice-an-epic.md). Slicing often surfaces gaps; fill each at its home
   before a slice cites it ([`./engineering/slices.md`](./engineering/slices.md)).
3. **File tracker work once every prerequisite can be named**: the slices or epics it depends on, the requirements it
   builds on, the open decisions it waits on. A filed slice records its tracker item in `external:`, and from then on
   the tracker owns its progress.
4. **Deliver and archive** with the epic's product side, through
   [`./workflows/deliver-an-epic.md`](./workflows/deliver-an-epic.md).

## Commit messages (planning:commit-messages)

Commits follow Conventional Commits. The scope is the epic or initiative id, with its project in a repo that has
projects (`docs(reliable-borrowing/reservations): …`, `docs(fleet/board): …`), or the project slug for a project-wide
change (`docs(fleet): …`). A program-wide change has no scope (`docs: …`).

- `feat` adds a registry row or a new requirements, spec, or slice file.
- `chore` is a status move or an archive move.
- `docs` is any other edit.

When a change moves work along its lifecycle, the body names the move: outline written, slices cut, epic in progress,
epic delivered and archived.

## Contribution checklists (planning:contributing)

Land each change through its checklist below, then [Before finishing](#before-finishing). The point is that every record
one change touches (a decision, the decision it overturns, the documents it corrects) lands together.

### Adding a document

1. Place it by the reader's question and the layout (`planning:placement`, `planning:layout`).
2. Run the admission test (`planning:document-admission`). If something already owns the subject, improve that instead.
3. Cite ids as plain text, and head every record it defines `<Name> (<id>)` (`planning:id-citations`).
4. In the same change, give it the name and place the layout sets, or link it from the document that owns its subject. A
   new epic or initiative folder gets its `epic.md` or `initiative.md` and its registry row together. In a repo with no
   product content, a folder for an epic planned in a tracker gets an `epic.md` pointing upstream
   (`planning:tracker-epic`).
5. Rewrite or delete whatever it overtakes (`planning:change-in-place`).

### Adding an engineering requirement

1. Confirm engineering owns it (`planning:classify-requirement`). If a user could notice it change, it belongs upstream
   or in an assumption; if it only describes how the code keeps a promise, it belongs in the spec.
2. If it only restates the product requirement it serves, write nothing (`planning:beyond-product`).
3. Find the epic it serves. A constraint that serves no product requirement goes to the epic, initiative, project, or
   program it binds (`planning:engineering-constraints`).
4. Mint the id and add a section headed by a short name and the bare id in parentheses to that level's `engineering.md`
   (`planning:requirement-ids`, `planning:owned-scoped-ids`), or a bullet under `## Brief requirements` when one
   sentence states it fully (`planning:brief-requirements`).
5. Write one or two sentences citing what it serves (`planning:requirement-record`). A new scheme needs a README scheme
   row; unstated intent needs an assumption first.
6. Add an `Acceptance:` list holding only what engineering can verify. Anything product can judge goes under the product
   requirement.

### Recording an assumption

1. Check upstream first. If an upstream id already states the intent, serve that instead.
2. Make sure it is product-shaped (`planning:assumption-record`). A technology constraint is an `engineering:`
   requirement and a technology choice is a `decision:`.
3. Mint the id and add its section, headed the same way, to the folder's `assumptions.md`. State in product terms what
   is assumed and why engineering had to assume it.
4. Cite it from each requirement that rests on it.

### Confirming or rejecting an assumption

Delete the record either way (`planning:assumption-lifecycle`). If it is confirmed, move the intent to its product home
in the same change and repoint every citation of the `assume:` id there. If it is rejected, re-derive or delete every
requirement that served only it, and fix every other citation (`planning:rejected-assumption`).

### Recording a decision

1. Check it clears the bar (`planning:decision-bar`); a clarification edits the requirement or spec instead.
2. Choose the owner, which fixes the file and the id's scope (`planning:decision-ownership`). Then choose a slug that is
   new in the owner's `decisions.md` (`planning:decision-slugs`) and at every level outward (`planning:no-shadowing`).
3. Write it in the owner's `decisions.md`, creating the file if needed, and leave it open if the call is deferred
   (`planning:decision-format`).
4. Making an open decision or overturning a made one rewrites its entry in place under the same id.
5. Rewrite or delete what it invalidates, fixing every citation of a deleted id, and cite the decision in each document
   it binds.

### Slicing an epic

Follow [`./workflows/slice-an-epic.md`](./workflows/slice-an-epic.md).

### Reviewing requirements

Follow [`./workflows/requirements-review.md`](./workflows/requirements-review.md) after product intent changes and
before slicing.

### Asking a clarifying question

Add a bullet to `## Open questions` at the end of the file it concerns (`planning:inline-questions`). Once it is
answered, fold the answer into the text and delete the bullet.

### Before finishing

- Every new document passes `planning:document-admission` and sits where `planning:layout` puts it.
- Every cited id resolves (`planning:id-citations`, `planning:bare-ids`), and none points at a deleted id
  (`planning:change-in-place`).
- No scoped id changed except through `planning:moving-ids`.
- Nothing breaks `planning:no-shadowing`, `planning:project-slugs`, or `planning:product-cites-product`.
- Every changed `epic.md` or `initiative.md` meets `planning:epic-frontmatter` or `planning:initiative-frontmatter`.
- Every milestone chart and ledger naming a changed epic is current (`planning:milestone-registry`,
  `planning:delivery-ledger`), and the epic's folder matches its status (`planning:delivered-archive`).
- Every slice still meets `planning:slice-files` and `planning:slice-order`.
- Nothing in `supporting/` was edited unless someone asked (`planning:layout`).
