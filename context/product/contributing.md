# Contributing product content

## Epic lifecycle (preq:lifecycle)

Every epic takes the same path from idea to delivered, and each step is a deliberate change rather than a drift:

1. **Row and epic together.** The epic's row in `epics.md` and its `epic.md` land in the same change, the file at
   `refinement: outline` with its frontmatter and at least one sentence of the problem (`preq:epic-registry`,
   `preq:epic-frontmatter`); an epic is never named without its file. A milestone demanding it enters first or with it.
2. **Deepen as the work gets close.** When work is weeks away, `epic.md` grows its outcome and `## Left for later`, and
   `requirements.md` its requirements and their acceptance bullets (`preq:requirement-records`); open calls become open
   decisions (`preq:decision-format`). The product owner re-grades refinement; an agent never chooses a grade and writes
   `outline` on anything it creates.
3. **Engineering derives.** Engineering writes its requirements, any assumptions, and the spec in the same folder, each
   citing the product requirement it serves. Product files never cite them back (`preq:product-cites-product`).
4. **File tracker work only once every prerequisite can be named** — landed already, or filed beside it. Engineering
   cuts the epic into the tracker items that build it. When work on the epic starts, its frontmatter moves to
   `status: in-progress`, and the same change sets its cell in every milestone chart naming it (`preq:epic-status`,
   `preq:milestone-registry`).
5. **Deliver and archive.** Evidence of delivery sets `status: delivered`, and that one change archives the epic and
   updates every registry naming it, following [`./workflows/deliver-an-epic.md`](./workflows/deliver-an-epic.md).

Turning an epic into an initiative, or moving an epic into or out of one, is a deliberate change of its own: it changes
the epic's id and every id scoped to it, and that change rewrites every citation in the repo (`preq:moving-ids`).

## Commit messages (preq:commit-messages)

<!-- shared:commit-messages -->

Commits follow Conventional Commits, scoped by the epic or initiative id they touch —
`docs(reliable-borrowing/reservations): …` — or by the root file for a program-wide change. Use `feat` for a new
registry row or a new requirements, spec, or slice file, `chore` for a status move or an archive move, and `docs` for
any other edit. When a change moves work along its lifecycle, the body says which move — outline written, slices cut,
epic in progress, epic delivered and archived.

<!-- /shared:commit-messages -->

## Contribution checklists (preq:contributing)

Land every product change through the matching checklist below, then the closing checks. Each step applies the rule it
cites; the checklist keeps the records one change touches — a decision, the decision it overturns, the documents it
corrects — landing together.

### Adding a document

1. Pick the place by the reader's question and the layout — `preq:placement`, `preq:layout`.
2. Run the admission test — `preq:document-admission`. If the subject is already owned, improve the owner.
3. Cite every id as plain text, and give every record it defines a `<Name> (<id>)` heading — `preq:id-citations`.
4. Give it the name and place the layout sets, or link it from the document owning its subject, in the same change —
   `preq:document-admission`. A new epic or initiative folder gets its `epic.md` or `initiative.md` and its registry row
   together.
5. Rewrite in place or delete what it overtakes — `preq:change-in-place`.

### Recording a decision

1. Check it clears the bar — `preq:decision-bar`. A clarification edits the requirement instead.
2. Choose the owner — `preq:decision-ownership` — which fixes the file and the id's scope; then the slug —
   `preq:decision-slugs` — checking the owner's `decisions.md` for a collision.
3. Write it in the owner's `decisions.md` — `preq:decision-format` — open if the call is deferred. A folder's first
   decision creates the file (`preq:decisions-file`).
4. When making an open decision or overturning a made one, rewrite its entry in place and keep the id.
5. Rewrite what it invalidates in place, or delete it, fixing every citation of a deleted id (`preq:change-in-place`);
   cite the decision in each document it binds.

### Asking a clarifying question

Add a bullet to the `## Open questions` at the end of the file it concerns — `preq:inline-questions`. When it is
answered, fold the answer into the text and delete the bullet.

### Before finishing

- Every new document sits where the layout names it, or is linked from the document owning its subject.
- Every cited id is plain text and appears verbatim in a real row, heading, or frontmatter field, and no heading is an
  id alone.
- No product-owned file cites an `engineering:` or `assume:` id or links an engineering file
  (`preq:product-cites-product`).
- Every changed `epic.md` or `initiative.md` still satisfies its frontmatter rule, every milestone chart naming a
  changed epic shows its status (`preq:milestone-registry`), and every newly reached milestone has moved to
  `delivered.md` (`preq:delivery-ledger`).
- An epic whose `status:` is `delivered` sits in `delivered/`; any other epic stays in `work/`.
- Nothing in `supporting/` was edited unless someone asked.
