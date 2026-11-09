# Layout

How a requirements repo is laid out, who owns each file, and where finished work goes. Every rule here binds both tiers.

## Repository layout (planning:layout)

A requirements repo is organized by product work, not by discipline. Under `work/` there is one folder per epic, named
by its epic slug: `work/<epic>/` for a standalone epic, `work/<initiative>/<epic>/` for one under an initiative. An
initiative folder is named by its initiative slug.

Files have the same names wherever they sit, so either framework can find a file without knowing whether the other is in
use. No file takes a name outside this table. An epic folder holds `epic.md` and whichever of the rest it needs; an
initiative folder holds `initiative.md`, its epic folders, and whichever of the rest apply to it.

| File              | Owner       | Holds                                                                          |
| ----------------- | ----------- | ------------------------------------------------------------------------------ |
| `epic.md`         | Product     | The epic's front door: frontmatter, problem, outcome, what it leaves for later |
| `initiative.md`   | Product     | The same, for an initiative                                                    |
| `requirements.md` | Product     | Product requirements; in an initiative folder, those binding every epic        |
| `engineering.md`  | Engineering | Engineering requirements                                                       |
| `assumptions.md`  | Engineering | Product-shaped intent engineering assumed in order to move forward             |
| `spec.md`         | Engineering | Designs and technical contracts                                                |
| `slices/`         | Engineering | The ordered changes that build the epic, one file each                         |
| `decisions.md`    | Shared      | Decisions of both tiers, open and made                                         |
| `research/`       | Shared      | Investigation local to the folder                                              |
| `assets/`         | Shared      | Non-markdown material: proofs of concept, sample configs, images, data         |
| `presentations/`  | Shared      | Material authored to be presented or published                                 |
| `mockups/`        | Product     | UI mockups; these never go in `assets/`                                        |

The repo root holds `README.md`, `work/`, `delivered/` once anything is delivered, the program's `decisions.md`, and the
program-wide product files (`planning:product-areas` in [`./structure.md`](./structure.md)). It also holds a
`requirements.md` when a product requirement binds every epic, an `engineering.md` when an engineering record binds the
whole system, and the shared `research/`, `presentations/`, and `supporting/` when there are any. A repo with projects
repeats this layout inside each project folder and keeps at its root only what binds the whole program
([`./projects.md`](./projects.md)).

`research/` holds findings and options that stop short of a choice, one `research/<subject>/` folder per subject, with
the scripts that produced the findings beside them. `supporting/` holds reference material authored outside the team and
is edited only when someone asks.

## File ownership (planning:file-ownership)

Each content file is owned by one tier or shared by both. An owned file follows only its own tier's rules. Shared files
and folders — `decisions.md`, `research/`, `assets/`, `presentations/`, `supporting/`, and the `epic.md` of an epic
planned in a tracker — have one format that binds both tiers, as does the layout itself. A repo may hold product
content, engineering content, or both.

## File or folder (planning:file-or-folder)

A document kind is either a single `<name>.md` while it is small or, once it grows, a `<name>/` folder of leaves, never
both at once. Leaves are named by subject, not by date or sequence, and the folder has no index beside them. Both forms
hold the same records under the same ids. Switching forms moves records without changing any id, and repoints every link
to the leaf that now holds its target in the same change.

`slices/` is the exception: it only exists as a folder, and its leaf names carry the build order. The `delivered/`
archive is not the folder form of the `delivered.md` ledger; the two sit side by side.

## Epics planned in a tracker (planning:tracker-epic)

An epic whose product intent lives in a work tracker still has an `epic.md`, so its status has a home in the repo. The
file holds the epic frontmatter, with `external:` naming the tracker epic, and one sentence saying the intent lives
there. Its folder has no `requirements.md`.

```markdown
---
epic: overdue-returns
refinement: outline
status: in-progress
external: jira:SHED-40
---

# Overdue returns

The product intent for this epic lives in its tracker epic; this file tracks its status.
```

Each `external:` value is one `<system>:<id>`, the same string an engineering requirement uses to cite the item. Status
moves as it does for any epic: `in-progress` when work starts, `delivered` once there is evidence it reached its users.
Either tier may write the file, since it records tracker state rather than intent. An agent writes
`refinement: outline`; only the product owner records another grade. In a repo holding only engineering content, this
rule alone shapes the file.

When all of a repo's product intent lives in a tracker, engineering writes each epic's `epic.md` as it files the epic's
work and keeps its `status:` in step with the tracker.

## Capability epics (planning:capability-epics)

Every requirement serving an epic lives in that epic's folder. A shared or platform capability that other epics rely on
is a product epic of its own, with its own folder under `work/`. Its intent says which initiatives or epics it supports
and why it exists, and its `epic.md` opens by naming them:

> Supports `epic:overdue-returns` and `epic:reliable-borrowing/reservations`: members hear about a due date or a lapsed
> reservation without checking the app.

Its engineering requirements live in its folder and derive from it, and may also cite the epics it supports. There are
no folders for services, components, or system areas.

When a requirement serves a shared capability that no epic owns yet, ask product for that epic rather than parking the
requirement in the first epic that needed it. In a repo with projects, the capability epic sits in the project that owns
the capability, and the others cite it by full id (`planning:cross-project` in [`./projects.md`](./projects.md)).

## Delivered archive (planning:delivered-archive)

The change that sets an epic's `status: delivered` also moves its folder with `git mv` from `work/` to `delivered/`,
keeping its shape (`delivered/<epic>/` or `delivered/<initiative>/<epic>/`), and repoints every relative link to or from
it. In a repo with projects, the move stays inside the epic's project. Everything in the folder moves, engineering
content included, and ids don't change, since no id names the `work/` or `delivered/` root.

A delivered folder is frozen as the record of what was promised and how it was to be built. Nothing in it changes
afterwards except a link a later change repoints, and nothing moves back: later work on a delivered capability is a new
epic.

An initiative stays in `work/` while it has live epics, and its finished epics move one at a time. The change that
delivers its last epic moves the rest of the folder, `initiative.md` included, to `delivered/<initiative>/`.
