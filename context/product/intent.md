# Epic and initiative intent

An epic folder's `epic.md` and an initiative folder's `initiative.md`, the front doors carrying a work folder's
frontmatter and intent: where an epic ends and an initiative begins, who sets each frontmatter value, how an epic's
status and refinement move, and the sections each file carries. The requirements they front are
[`./requirements.md`](./requirements.md).

## Epic or initiative (preq:epic-or-initiative)

An epic has a problem of its own: it could be prioritized, deferred, or dropped without changing why any other epic
exists, and it is delivered as a whole. When part of an epic needs to be prioritized, tracked, or delivered on its own,
that part is an epic too, and the epics sharing the problem form an initiative; the change that makes the cut rewrites
every citation of the old id (`preq:moving-ids` in [`./namespaces.md`](./namespaces.md)). In the team's work tracker an
epic is one epic. How it is built — the changes engineering cuts it into, each one tracker item under the epic — is
engineering's to write and the tracker's to follow, and product files never name them. An epic with only a few sentences
of its own is probably part of another, and an epic whose parts each need a status of their own is an initiative.

## Epic frontmatter (preq:epic-frontmatter)

Every epic's `epic.md` begins with this frontmatter, then states the epic's intent (`preq:product-sections`):

```yaml
---
epic: volunteer-shifts          # required; the epic id, matching epic:<id>
refinement: refined             # required; outline | refined | final
status: in-progress             # required; planned | in-progress | delivered
external: jira:SHED-50          # optional; the epic in another system, one <system>:<id>
---
```

`external:` names the item standing for the epic in another system — its tracker epic, a portfolio item, a wiki page —
as one `<system>:<id>` scalar, written exactly as it is cited: `jira:SHED-50`, `linear:LN-995`, `github:shed#43`.
`<system>` names the system in lowercase, whichever the team uses, and `<id>` is the item's key as that system writes
it, the same string engineering cites the item by. Only in the rare case of more than one item is the value a list,
`external: [jira:SHED-50, linear:LN-995]`. Values are identifiers only; when a key moves, update it in place. An epic
planned in a tracker carries the same frontmatter in an `epic.md` holding nothing else, its `external:` naming the
tracker epic (`preq:tracker-epic` in [`./layout.md`](./layout.md)).

## Initiative frontmatter (preq:initiative-frontmatter)

An initiative's frontmatter sits in its `initiative.md`, the folder's front door, which then states the initiative's
intent (`preq:product-sections`).

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

`external:` takes the epic's form (`preq:epic-frontmatter`). The `epics:` list holds names only; each epic's status
lives in its own frontmatter. An initiative has no status of its own: it is finished when every epic in it is delivered.
The body cites the epics it discusses but repeats neither their order nor their state. Its refinement judges the intent
and the cut into epics, independently of each epic's. A `requirements.md` beside it is optional and holds only
`product:` records binding every epic in the initiative; with none, the file is not written.

## Epic status and refinement (preq:epic-status)

Epic status is coarse product state, set by these events and no others: work on the epic starting in the work tracker
sets `in-progress`; evidence that the epic reached its users sets `delivered`, in the one change
[`./workflows/deliver-an-epic.md`](./workflows/deliver-an-epic.md) lays out. An epic filed in the tracker but not yet
started stays `planned`. The repo records only the epic's status, set by whoever runs the work as the epic moves; the
tracker owns the progress of everything inside it. New intent starts `refinement: outline`, and an agent always writes
`outline`, never choosing a grade; `refined` means the intent is settled enough to build from. Only the product owner
records `refined` or `final`, `final` when they declare the intent complete — the epic being `delivered` may prompt that
judgment but does not make it. The committed value is the record of that judgment; no separate sign-off artifact is
needed. Each fact has one source:

| Concern                                            | Source of truth                                                            |
| -------------------------------------------------- | -------------------------------------------------------------------------- |
| An epic's status                                   | The frontmatter of the epic's `epic.md`, a tracker-planned epic's included |
| An initiative's epics, ordered                     | The frontmatter of the initiative's `initiative.md`                        |
| What each unreached milestone needs                | `milestones.md`                                                            |
| Work-item workflow, and progress inside an epic    | The work tracker                                                           |
| Ids in other systems                               | The `external:` frontmatter of the epic or initiative                      |
| The milestones reached, and what each epic covered | `delivered.md`                                                             |
| Refinement                                         | The product owner, recorded in frontmatter                                 |
| Decisions, open and made                           | Their owners' `decisions.md`                                               |

## Product sections (preq:product-sections)

After its frontmatter, an `epic.md` holds, in order:

1. A `#` title, then one line naming the parent initiative, if any, and where the product requirements live; a
   capability epic's line also names what it supports (`preq:capability-epics` in [`./layout.md`](./layout.md)).
2. `## The problem` — whose work is hard and what that costs. An outline epic may hold just a sentence of it and nothing
   after, growing the rest as the work gets close (`preq:lifecycle` in [`./contributing.md`](./contributing.md)).
3. `## The outcome` — what is different for them once the work lands.
4. Optional: `## Left for later`, each deferral naming the epic or initiative that owns it, so a reader can tell a gap
   from an oversight; `## What this epic is not`, what a reader might expect of it that it deliberately leaves undone
   and no later work is planned to do; `## Depends on`, product ids only; the requirement records inline under
   `## Requirements`, for a small epic (`preq:requirement-records` in [`./requirements.md`](./requirements.md));
   `## Open questions` (`preq:inline-questions` in [`./decisions.md`](./decisions.md)).

Never: status prose repeating the frontmatter; a stories or slices table, or a `delivery/` folder; epic-level
acceptance, "Complete when", or "How it is proven", since each requirement carries its own acceptance bullets
(`preq:requirement-acceptance` in [`./requirements.md`](./requirements.md)); a "What to build" list, which the
requirement records are; an engineering id (`preq:product-cites-product` in [`./namespaces.md`](./namespaces.md)). An
epic planned in a tracker follows `preq:tracker-epic` in [`./layout.md`](./layout.md) instead.

After its frontmatter, an `initiative.md` holds, in order:

1. A `#` title, then a one-sentence opener.
2. `## The problem`.
3. `## The outcome`, naming its epics in prose.
4. Optional: `## Left for later`; `## Stance`, the rules every epic in it must keep.

Never: an epics table or list, which the frontmatter holds; status; build order; `product:` records.
