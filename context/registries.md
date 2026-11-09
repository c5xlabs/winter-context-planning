# Product registries

A repo holding product content keeps four registries — `initiatives.md`, `epics.md`, `milestones.md`, and `delivered.md`
— at its root, or in each project folder when the repo has projects. Each opens with one product-voice paragraph saying
what the file is and that it is not a status board; that paragraph carries no status, dates, or epic list. The sections
below say what comes after it.

## Registries across projects (planning:registry-levels)

In a repo with [projects](./projects.md), each project folder keeps its own registries for its own work, linking into
that project's `work/` and `delivered/`. The program root holds no work, so it has no `epics.md` or `initiatives.md`;
its `milestones.md` and `delivered.md` hold only destinations that belong to the program rather than to any one project.

A milestone lives at the level whose destination it is, never at both. A chart row citing an epic or initiative from
another project uses its full id. The program's `delivered.md` has no `## Outside the milestones` section: an epic that
serves no milestone is recorded in its own project's ledger.

## Initiative registry (planning:initiative-registry)

A repo that uses initiatives keeps `initiatives.md`. An initiative is a durable product investment broader than one
capability; it can own work directly and contain epics. After the opening paragraph comes one table,
`Initiative | Outcome`:

- **Initiative** is the stable `initiative:<slug>` id, linked to the initiative's owning doc: its
  `work/<initiative>/initiative.md` (`planning:initiative-frontmatter`) or its declared external home
  (`planning:repository-entry`). Once its last epic settles, the link points into `delivered/`.
- **Outcome** is the shared product result, not a project phase, team, or mechanism.

Rows carry nothing else: no status, dates, tracker keys, epic list, or links to supporting material.

```markdown
| Initiative                                                                 | Outcome                                                                                                      |
| -------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| [`initiative:reliable-borrowing`](./work/reliable-borrowing/initiative.md) | A member who reserves a tool finds it waiting, and the next member finds it back on the shelf when it is due |
```

## Epic registry (planning:epic-registry)

A repo holding product content keeps `epics.md`, the capabilities the product still intends to build. After the opening
paragraph comes one table, `Epic | Capability`, in product-priority order; the order changes only through a deliberate
reprioritization.

- **Epic** is the stable `epic:<slug>` id (`epic:<initiative>/<epic>` under an initiative), and is the row's one link,
  to the epic's `epic.md`. For an epic planned in a tracker, that `epic.md` names the tracker item
  (`planning:tracker-epic`).
- **Capability** is the row's only prose. It starts with the person, problem, and promise before any mechanism. A
  durable constraint on the capability belongs here; a relationship to other work does not.

Rows carry no status, dates, tracker keys, horizons, milestones served, dependencies, gating, or scope rationale. Status
lives in the epic's frontmatter (`planning:epic-frontmatter`), the tracker owns workflow, and the rest goes in
`epic.md`.

Every epic is needed by at least one milestone, directly or through its initiative; an epic that isn't uses its
Capability cell to state the operational necessity that justifies it. Naming an epic writes its row and its `epic.md`
together (`planning:lifecycle`); opening tracker work doesn't change the row. A delivered epic loses its row, and its id
resolves to its `epic.md` in `delivered/`.

```markdown
| Epic                                                                                     | Capability                                                                                                                                                                      |
| ---------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [`epic:reliable-borrowing/reservations`](./work/reliable-borrowing/reservations/epic.md) | A member who reserved a tool and never came should not keep it off the shelf for a week, and a member who wants a tool already reserved should hear the moment it frees up.     |
| [`epic:volunteer-shifts`](./work/volunteer-shifts/epic.md)                               | A volunteer should sign up for a shift in the app and see who is coming during it, so the coordinator stops keeping the roster in a shared spreadsheet that members cannot see. |
```

## Milestone registry (planning:milestone-registry)

A repo holding product content keeps `milestones.md`, where product planning starts: each milestone states a destination
in a person's work and names the epics needed to reach it. The file holds only unreached milestones, one section each,
in the order they are meant to be reached. The headings are the list; there is no summary table.

Each section is headed `## <Name> (milestone:<slug>)` with a stable slug, and until the milestone is reached that
heading is the id's only home. It holds a short product-voice paragraph saying what people will be able to do once it is
reached — something observable in their work, not a feature, an implementation, or a date — then a chart
`Epic | Status`. Each row is one epic, its id as plain text, or one initiative when the milestone needs all of it. An
epic can serve several milestones.

An epic's Status is its own `status:` (`planning:epic-status`), updated in the same change that moves the epic; when the
two disagree, the epic is right and the cell gets corrected. An initiative's row is `delivered` once all its epics are,
`in-progress` once any is in progress or delivered, and `planned` otherwise.

A milestone enters before or with the epics it needs. It is reached when every row is `delivered`, and the change that
delivers the last one moves its section into `delivered.md`.

```markdown
## Reserve ahead (milestone:reserve-ahead)

A member sees from home whether a tool is in, reserves it for a pickup window, and finds it set aside on the pickup
shelf when the window starts.

| Epic                                   | Status      |
| -------------------------------------- | ----------- |
| `epic:reliable-borrowing/availability` | delivered   |
| `epic:reliable-borrowing/reservations` | in-progress |
```

## Delivery ledger (planning:delivery-ledger)

A repo holding product content keeps `delivered.md`, the durable record of reached milestones, newest first. A section
moved here keeps its heading, which becomes the milestone id's home, and holds one sentence of what people can now do
and an `Epic | Notes` table: the chart's rows, each Notes cell saying in a few words what that epic covered. There are
no dates; git records when a section moved.

The ledger ends with `## Outside the milestones`, in the same shape, for delivered epics that served no milestone; the
change that delivers such an epic adds its row. Omit the section when it would be empty. An empty ledger is just its
heading and opening paragraph. Correct factual errors, but don't rewrite history into later vocabulary.

The ledger is not the `delivered/` archive (`planning:delivered-archive`), which takes an epic's folder when the epic is
delivered, whether or not any milestone it serves is reached.

```markdown
## Reserve ahead (milestone:reserve-ahead)

A member reserves a tool from home and finds it set aside on the pickup shelf when their window starts.

| Epic                                   | Notes                                                |
| -------------------------------------- | ---------------------------------------------------- |
| `epic:reliable-borrowing/availability` | Whether each tool is in, visible from home           |
| `epic:reliable-borrowing/reservations` | Pickup windows, release on no-show, and the waitlist |

## Outside the milestones

| Epic                | Notes                                                           |
| ------------------- | --------------------------------------------------------------- |
| `epic:loan-history` | Every checkout and return traceable to a volunteer and a member |
```
