# Layout

How a requirements repo is laid out: the `work/` and `delivered/` trees, owned and shared files, file-or-folder forms,
the folder front door, an epic planned in a tracker, where a shared capability goes, and how finished work is archived.
Every rule here is shared word for word with the Engineering Requirements Framework.

## Repository layout (preq:layout)

<!-- shared:layout -->

Organize a requirements repo by product work, not by discipline: under `work/`, one folder per epic, named by its epic
slug — `work/<epic>/` for a standalone epic, `work/<initiative>/<epic>/` for one under an initiative. A folder holding
epic folders is an initiative folder, named by its initiative slug. Every file has the same name wherever it sits, so
either framework finds a file without knowing whether the other is in use, and no file takes a name outside this table.
An epic folder holds `epic.md`, its front door, and whichever of the rest it needs; an initiative folder holds
`initiative.md`, its front door, its epic folders, and the subset that applies to it:

| File              | Owner                                    | Holds                                                                                       |
| ----------------- | ---------------------------------------- | ------------------------------------------------------------------------------------------- |
| `epic.md`         | Product; shared for an epic in a tracker | The epic's frontmatter, problem, outcome, and what it leaves for later                      |
| `initiative.md`   | Product                                  | The initiative's frontmatter, problem, outcome, and what it leaves for later                |
| `requirements.md` | Product                                  | An epic's product requirements; in an initiative folder, any requirement binding every epic |
| `engineering.md`  | Engineering                              | Engineering requirements                                                                    |
| `assumptions.md`  | Engineering                              | Product-shaped intent engineering assumed to move forward                                   |
| `spec.md`         | Engineering                              | Designs and technical contracts                                                             |
| `slices/`         | Engineering                              | The epic's slices: the ordered changes that build it, one file each                         |
| `decisions.md`    | Shared                                   | Decisions of both tiers, open and made                                                      |
| `research/`       | Shared                                   | Investigation local to the folder, optional                                                 |
| `assets/`         | Shared                                   | Non-markdown material: proofs of concept, sample configs, images, data                      |
| `presentations/`  | Shared                                   | Material authored to be presented or published, on any subject, optional                    |
| `mockups/`        | Product                                  | UI mockups, optional; a mockup never goes in `assets/`                                      |

The root holds `README.md`, `work/`, `delivered/` once anything is delivered, the program's `decisions.md`, its
`engineering.md` when a constraint binds the whole system, the shared `research/`, `presentations/`, and `supporting/`
when present, and the program-wide files the Product Requirements Framework names; it holds no `requirements.md`.
`research/` holds findings and options stopping short of a choice, one `research/<subject>/` folder per subject with the
scripts that produced them beside the findings; `supporting/` holds reference material authored outside the team, edited
only when someone asks. A repo whose product intent lives in a tracker uses the same tree: each epic folder's `epic.md`
carries its status and names the tracker epic in its `external:` frontmatter, and the folder holds no `requirements.md`.

<!-- /shared:layout -->

## File ownership (preq:file-ownership)

<!-- shared:file-ownership -->

No content file is governed by both frameworks: an owned file is shaped only by its one governing framework. A shared
file — `decisions.md` and the `epic.md` of an epic planned in a tracker — or shared folder — `research/`, `assets/`,
`presentations/`, `supporting/` — has one format, set by a rule both frameworks carry word for word. The layout is
itself a shared rule. This keeps either framework adoptable alone.

<!-- /shared:file-ownership -->

## File or folder (preq:file-or-folder)

<!-- shared:file-or-folder -->

Every document kind takes one of two forms, never both side by side: `<name>.md` while it is small, or a `<name>/`
folder of `<name>/*.md` leaves once it grows, each named by its subject, never by date or sequence, with no index or hub
beside them. Both forms hold the same records under the same ids; switching forms moves records, repoints every link to
the leaf that now holds its target in the same change, and never changes an id. The `delivered/` archive is not the
folder form of the `delivered.md` ledger; the two sit side by side. `slices/` is the one exception: it has only the
folder form, and its leaves carry their build order in their names.

<!-- /shared:file-or-folder -->

## Epics planned in a tracker (preq:tracker-epic)

<!-- shared:tracker-epic -->

An epic whose product intent lives in a work tracker still has an `epic.md`, so its status has one home in the repo. It
holds the epic frontmatter, whose `external:` names the tracker epic carrying the intent, then one short sentence saying
the intent lives there, and nothing else:

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

Each `external:` value is one `<system>:<id>`, the same string an engineering requirement cites the item by upstream.
The status moves on the same events as any epic's: work starting on the epic sets `in-progress`, and evidence it reached
its users sets `delivered`. Either tier may write the file, because it records tracker state rather than intent; an
agent writes `refinement: outline`, and only the product owner records another grade. A repo following only the
Engineering Requirements Framework shapes the file by this rule alone.

<!-- /shared:tracker-epic -->

## Capability epics (preq:capability-epics)

<!-- shared:capability-epics -->

Every requirement serving an epic lives in that epic's folder. A shared or platform capability other epics rely on is a
product epic in its own right: it has its own folder under `work/`, and its intent — its `epic.md`, or the tracker item
that file points at — states which initiatives or epics it supports and why it exists. Engineering requirements for it
live in its folder and derive from it, and may also cite the epics it supports. No folder exists for a service,
component, or system area. Making the capability an epic gives it an owner who says what it must do and when it is done.

<!-- /shared:capability-epics -->

A capability epic's `epic.md` opens by naming what it supports: *"Supports `epic:overdue-returns` and
`epic:reliable-borrowing/reservations`: members hear about a due date or a lapsed reservation without checking the
app."*

## Delivered archive (preq:delivered-archive)

<!-- shared:delivered-archive -->

When an epic's `epic.md` frontmatter sets `status: delivered`, its folder moves with `git mv` from `work/` to
`delivered/`, keeping its shape — `delivered/<epic>/`, or `delivered/<initiative>/<epic>/` — in the same change that
sets the status, and that change repoints every relative link to or from it. Nothing moves back: later work on a
delivered capability is a new epic. A delivered folder is frozen: it records what was promised and how it was to be
built when the epic was delivered, and nothing in it changes afterwards except a citation or link a later change
repoints. Ids never name the `work/` or `delivered/` root, so the move changes none. An initiative with live epics stays
in `work/` while its finished epics move one at a time; the change that delivers its last epic moves the rest of its
folder, `initiative.md` included, to `delivered/<initiative>/`.

<!-- /shared:delivered-archive -->
