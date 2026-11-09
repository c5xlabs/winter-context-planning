# Projects

The optional project level, for one requirements repo planning several products of one program. How ids carry a project
is [`./namespaces.md`](./namespaces.md).

## The program and its projects (planning:projects)

A requirements repo plans one program. A program whose products share personas, contracts, or requirements but are
planned and delivered apart divides into projects, one folder each at `projects/<project>/`, named by its project slug.
The taxonomy runs program, project, initiative, epic, slice: the program states what binds everything in it, each
project plans one product, and initiatives, epics, and slices sit inside a project as they sit in a repo without
projects. Every level may hold requirements, each binding everything beneath it.

Projects are optional, and a repo planning one product has none: it has no `projects/` folder, its root takes the layout
of `planning:layout` in [`./layout.md`](./layout.md), and nothing in this file applies to it. A repo with projects has
at least two. The set of projects is the listing of `projects/` and the README's Contents rows naming each one
(`planning:repository-entry` in [`./repository-entry.md`](./repository-entry.md)); there is no project registry.

A project is named by the product it plans, never a team, phase, or technology. The level is a project, not a product,
because `product:` already names a product requirement.

## The program root (planning:program-root)

In a repo with projects, the root holds what binds the whole program and no work of its own:

| Path                                         | R/O | Holds                                                                                               |
| -------------------------------------------- | --- | --------------------------------------------------------------------------------------------------- |
| `README.md`                                  | R   | The repo's one README (`planning:repository-entry`); no project carries its own                     |
| `charter/`                                   | R   | The program's charter (`planning:charter-levels` in [`./charter.md`](./charter.md))                 |
| `projects/`                                  | R   | One folder per project (`planning:project-folder`)                                                  |
| `requirements.md`                            | O   | `product:` records binding every epic in the program                                                |
| `engineering.md`                             | O   | `engineering:` records binding the whole program                                                    |
| `decisions.md`                               | O   | Decisions across projects, or that no project owns                                                  |
| `milestones.md`                              | O   | Destinations that are the program's, not any one project's                                          |
| `delivered.md`                               | O   | The program milestones reached, once there are any                                                  |
| `strategy/`                                  | O   | Direction-setting papers (`planning:product-areas` in [`./structure.md`](./structure.md))           |
| `mockup-kit/`                                | O   | The one kit every project's mockups share (`planning:mockup-kit` in [`./mockups.md`](./mockups.md)) |
| `research/`, `presentations/`, `supporting/` | O   | As at the root of a repo without projects (`planning:layout`)                                       |

The root holds no `work/`, `delivered/` archive, `epics.md`, or `initiatives.md`: every epic belongs to a project.

## The project folder (planning:project-folder)

A project folder takes the root layout of a repo without projects (`planning:layout`), minus what only the program
holds:

| Path                                        | R/O | Holds                                                                                                    |
| ------------------------------------------- | --- | -------------------------------------------------------------------------------------------------------- |
| `charter/`                                  | R   | The project's charter (`planning:charter-levels`); `mission.md` is the project's front door              |
| `epics.md`, `milestones.md`, `delivered.md` | R   | The project's registries and ledger (`planning:registry-levels` in [`./registries.md`](./registries.md)) |
| `initiatives.md`                            | O   | The project's initiative registry, when it uses initiatives                                              |
| `requirements.md`, `engineering.md`         | O   | Records binding every epic in the project                                                                |
| `decisions.md`                              | O   | Decisions across the project's epics, or that no epic owns                                               |
| `work/`, `delivered/`                       | R   | The project's epic and initiative folders, live and archived                                             |
| `research/`, `presentations/`               | O   | Material local to the project                                                                            |

It never holds a `README.md`, `strategy/`, `mockup-kit/`, or `supporting/`, which belong to the program.

An epic's folder sits at `projects/<project>/work/<epic>/`, or `projects/<project>/work/<initiative>/<epic>/` under an
initiative, and moves to the matching path under the project's `delivered/` (`planning:delivered-archive` in
[`./layout.md`](./layout.md)).

## Project slugs (planning:project-slugs)

A project slug is reserved across the repo: no initiative, epic, or program-level record of any prefix takes a project's
slug as its own, so the first segment of any id that matches a project slug always names that project
(`planning:owned-scoped-ids` in [`./namespaces.md`](./namespaces.md)). A project slug is never renamed or reused, like
every product id (`planning:stable-product-ids`).

**Detect.** An initiative, standalone epic, persona, job, milestone, or program-level `product:`, `engineering:`, or
`decision:` subject whose slug is a project's.

## Work shared across projects (planning:cross-project)

Each record lives at the narrowest level it binds: an epic or initiative, a project, or the program. A requirement,
constraint, or decision binding more than one project, or a milestone that is no one project's destination, belongs to
the program. A capability several projects build on is a capability epic in the project that owns it
(`planning:capability-epics` in [`./layout.md`](./layout.md)), never at the program root, which holds no work; other
projects cite it by its full id. Where a persona or job lives is `planning:charter-levels` in
[`./charter.md`](./charter.md). Nothing shared is copied into a second project.

Moving an epic or initiative from one project to another, or a record from a project to the program, changes its id
(`planning:moving-ids` in [`./namespaces.md`](./namespaces.md)).
