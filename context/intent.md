# Epic and initiative intent

An epic folder's `epic.md` and an initiative folder's `initiative.md` are the folder's front doors: each carries its
frontmatter and states its intent. The requirements they front follow [`./requirements.md`](./requirements.md).

## Epic or initiative (planning:epic-or-initiative)

An epic has a problem of its own (it could be prioritized, deferred, or dropped without changing why any other epic
exists) and is delivered as a whole. When part of an epic needs to be prioritized, tracked, or delivered on its own,
that part becomes an epic too, and the epics sharing the problem form an initiative. The change that makes the cut
rewrites every citation of the old id (`planning:moving-ids`).

An epic with only a few sentences of its own probably belongs to another. An epic whose parts each need their own status
is an initiative.

In the work tracker an epic is one epic. The changes engineering cuts it into, one tracker item each, are engineering's
to write and the tracker's to follow; product files never name them.

## Epic frontmatter (planning:epic-frontmatter)

Every `epic.md` begins with this frontmatter:

```yaml
---
epic: volunteer-shifts          # required; the epic id, matching epic:<id>
refinement: refined             # required; outline | refined | final
status: in-progress             # required; planned | in-progress | delivered
external: jira:SHED-50          # optional; the epic in another system, one <system>:<id>
---
```

`external:` names the item standing for the epic in another system, such as a tracker epic, a portfolio item, or a wiki
page, written exactly as it is cited: `jira:SHED-50`, `linear:LN-995`, `github:shed#43`. The system name is lowercase,
and the id is the key as that system writes it, the same string engineering cites. Use a list,
`external: [jira:SHED-50, linear:LN-995]`, only when there is more than one item. Values are identifiers only; when a
key moves, update it in place.

An epic planned in a tracker still has an `epic.md`, holding this frontmatter and nothing else, with `external:` naming
the tracker epic (`planning:tracker-epic`).

## Initiative frontmatter (planning:initiative-frontmatter)

Every `initiative.md` begins with this frontmatter:

```yaml
---
initiative: reliable-borrowing  # required; matches initiative:<slug> and the folder name
refinement: outline             # required; outline | refined | final
external: [jira:SHED-12, linear:LN-995]  # optional; one <system>:<id>, a list only when there are several
epics:                          # required; every member epic, delivered ones included
  - availability                # each epic's own slug, in the order they are meant to land
  - reservations
  - deposits
---
```

`external:` works as it does for an epic. `epics:` holds names only. An initiative has no status: each epic's lives in
its own frontmatter, and the initiative is finished when every epic in it is delivered. The body cites the epics it
discusses but doesn't repeat their order or state. The initiative's refinement judges its intent and its cut into epics,
independently of each epic's.

A `requirements.md` beside it is optional and holds only `product:` records that bind every epic in the initiative.

## Epic status and refinement (planning:epic-status)

Status is coarse product state, and only two events move it. Work on the epic starting in the tracker sets
`in-progress`. Evidence that the epic reached its users sets `delivered`, in the one change
[`./workflows/deliver-an-epic.md`](./workflows/deliver-an-epic.md) lays out. An epic filed in the tracker but not yet
started stays `planned`. Whoever runs the work updates the status; progress inside the epic belongs to the tracker.

New intent starts at `refinement: outline`, and an agent always writes `outline`. `refined` means the intent is settled
enough to build from; `final` means the product owner has declared it complete. Only the product owner records either,
and the committed value is the sign-off. An epic being `delivered` may prompt the call to `final` but doesn't make it.

Each fact has one source:

| Fact                                               | Source                                                |
| -------------------------------------------------- | ----------------------------------------------------- |
| An epic's status and refinement                    | Its `epic.md` frontmatter, tracker-planned epics too  |
| An initiative's epics, in order                    | Its `initiative.md` frontmatter                       |
| What each unreached milestone needs                | `milestones.md`                                       |
| Work-item workflow, and progress inside an epic    | The work tracker                                      |
| Ids in other systems                               | The `external:` frontmatter of the epic or initiative |
| The milestones reached, and what each epic covered | `delivered.md`                                        |
| Decisions, open and made                           | Their owners' `decisions.md`                          |

## Product sections (planning:product-sections)

After its frontmatter, an `epic.md` holds, in order:

1. A `#` title, then one line naming the parent initiative, if any, and where the product requirements live. A
   capability epic's line also names what it supports (`planning:capability-epics`).
2. `## The problem`: whose work is hard and what that costs. An outline epic may hold just a sentence of it and nothing
   after, growing the rest as the work gets close (`planning:lifecycle`).
3. `## The outcome`: what is different for them once the work lands.

Any of these may follow:

- `## Left for later`, each deferral naming the epic or initiative that owns it.
- `## What this epic is not`, for what a reader might expect that the epic deliberately leaves undone, with no later
  work planned to do it.
- `## Depends on`, product ids only.
- `## Requirements`, holding the requirement records inline, for a small epic (`planning:requirement-records`).
- `## Open questions` (`planning:inline-questions`).

An epic doesn't carry status prose, a stories or slices table, a `delivery/` folder, or epic-level acceptance such as
"Complete when" or "How it is proven"; each requirement carries its own acceptance bullets
(`planning:requirement-acceptance`). Nor does it carry a "What to build" list, which the requirement records already
are, or an engineering id (`planning:product-cites-product`). An epic planned in a tracker follows
`planning:tracker-epic` instead.

After its frontmatter, an `initiative.md` holds, in order:

1. A `#` title, then a one-sentence opener.
2. `## The problem`.
3. `## The outcome`, naming its epics in prose.
4. Optionally, `## Left for later` and `## Stance`, the rules every epic in it must keep.

It doesn't carry an epics list, status, build order, or `product:` records.
