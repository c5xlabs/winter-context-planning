# Product registries

The four registries at the repo root: `initiatives.md`, `epics.md`, `milestones.md`, and `delivered.md`. Each opens with
one paragraph in the product voice saying what the file is and that it is not a status board, and that paragraph carries
no status, dates, or epic list; each rule below says what follows it.

## Initiative registry (preq:initiative-registry)

A repo that uses initiatives carries `initiatives.md`; a repo with none omits it. An initiative is a durable product
investment broader than one capability; it may own work directly and may contain epics. After the opening paragraph
comes one table `Initiative | Outcome`:

- Initiative: a stable `initiative:<slug>` id, itself the link to the initiative's owning doc —
  `work/<initiative>/initiative.md`, whose frontmatter lists its epics and whose body owns the problem, the outcome, and
  what it leaves for later (`preq:initiative-frontmatter`), or the initiative's declared external home
  (`preq:repository-entry`). Once its last epic settles, the link points into `delivered/`.
- Outcome: the shared product result — never a project phase, team, or mechanism.

Rows carry no status, dates, tracker keys, epic list, or supporting-material links: the registry says which investments
exist and what each is for, and everything else has its own home.

```markdown
| Initiative                                                                 | Outcome                                                                                                      |
| -------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------ |
| [`initiative:reliable-borrowing`](./work/reliable-borrowing/initiative.md) | A member who reserves a tool finds it waiting, and the next member finds it back on the shelf when it is due |
```

## Epic registry (preq:epic-registry)

A repo holding product content carries `epics.md`: the capabilities the product still intends to build, as a reference
registry. After the opening paragraph comes one table `Epic | Capability`, ordered by product priority; the order
changes only through a deliberate reprioritization. Each row holds these facts and no other — no status, dates, tracker
keys, horizons, milestones served, dependencies, gating, or scope rationale. Status lives in epic frontmatter
(`preq:epic-frontmatter`), the work tracker owns workflow, and the rest belongs in the epic's `epic.md`.

- Epic: a stable `epic:<slug>` id, itself the one link to the epic's `epic.md`, the home of its id — for an epic planned
  in a tracker, the `epic.md` naming the tracker item (`preq:tracker-epic`).
- Capability: the row's only prose, starting with the person, problem, and promise before any mechanism. A durable
  constraint on the capability belongs here; a relationship to other work does not.

Every epic is needed by at least one milestone, directly or through its initiative, or its Capability cell states the
operational necessity that justifies it without a destination.

A milestone creates the demand for an epic, and naming an epic writes its row and its `epic.md` together
(`preq:lifecycle` in [`./contributing.md`](./contributing.md)). Opening tracker work does not change the row. A
delivered epic has no row; its id still resolves at its `epic.md` in `delivered/`. An epic under an initiative is listed
by its full id, `epic:<initiative>/<epic>`.

```markdown
| Epic                                                                                     | Capability                                                                                                                                                                      |
| ---------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [`epic:reliable-borrowing/reservations`](./work/reliable-borrowing/reservations/epic.md) | A member who reserved a tool and never came should not keep it off the shelf for a week, and a member who wants a tool already reserved should hear the moment it frees up.     |
| [`epic:volunteer-shifts`](./work/volunteer-shifts/epic.md)                               | A volunteer should sign up for a shift in the app and see who is coming during it, so the coordinator stops keeping the roster in a shared spreadsheet that members cannot see. |
```

## Milestone registry (preq:milestone-registry)

A repo holding product content carries `milestones.md`, the top-down origin of product planning: each milestone states a
destination in a person's work and names the epics required to reach it. The file holds only milestones not yet reached.
After the opening paragraph comes one section per milestone, in the order they are meant to be reached, headed
`## <Name> (milestone:<slug>)` (`preq:id-citations`). Each section holds a short product-voice paragraph saying what
people will be able to do once it is reached, then a chart `Epic | Status`: one row per epic, its id as plain text, or
one row for an initiative when the milestone needs all of it. There is no summary table; the headings are the list.

The milestone id is stable, and until the milestone is reached its section here is the id's only home. The destination
is observable in a person's work, never a feature, an implementation, or a date. Status is the epic's own `status:`
(`preq:epic-status`). An initiative's row is `delivered` once every epic in it is, `in-progress` once any of them is in
progress or delivered, otherwise `planned`. The cell is kept in step with the epic, in the same change that moves the
epic's status; when the two disagree, the epic is the source, so correct the cell. One epic may serve several
milestones.

A milestone enters before or with the epics it needs. It is reached when every row is `delivered`, and the change that
delivers the last of them moves its section into `delivered.md`.

```markdown
## Reserve ahead (milestone:reserve-ahead)

A member sees from home whether a tool is in, reserves it for a pickup window, and finds it set aside on the pickup
shelf when the window starts.

| Epic                                   | Status      |
| -------------------------------------- | ----------- |
| `epic:reliable-borrowing/availability` | delivered   |
| `epic:reliable-borrowing/reservations` | in-progress |
```

## Delivery ledger (preq:delivery-ledger)

A repo holding product content carries `delivered.md`, the durable record of the milestones reached. After the opening
paragraph comes one section per reached milestone, newest first, as `preq:milestone-registry` moves it here. A moved
section keeps its `## <Name> (milestone:<slug>)` heading, which from then on is the milestone id's home, then holds one
sentence of what people can now do and a table `Epic | Notes`, the chart's rows with the Status column replaced: each
Notes cell says in a few words what that epic covered. An epic may appear under more than one milestone. There are no
dates; git records when a section moved.

The ledger closes with `## Outside the milestones`, in the same `Epic | Notes` shape: each delivered epic that served no
milestone, added by the change that delivers it. The section is absent when there are none. An empty ledger holds only
its heading and opening paragraph, never placeholder history. Entries are append-mostly: correct factual errors, but
never reshape history to later vocabulary.

The ledger is not the `delivered/` archive (`preq:delivered-archive` in [`./layout.md`](./layout.md)), which takes an
epic's folder when the epic is delivered, whether or not a milestone it serves is reached.

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
