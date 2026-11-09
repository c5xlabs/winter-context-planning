# Projects

Projects are an optional level for a requirements repo that plans several products of one program. How an id carries its
project is covered in [namespaces.md](./namespaces.md).

## The program and its projects (planning:projects)

A requirements repo plans one program. When the program's products share personas, contracts, or requirements but are
planned and delivered separately, the program divides into projects, each in its own folder at `projects/<project>/`
named by its slug. The levels run program, project, initiative, epic, slice. The program states what binds everything in
it, each project plans one product, and initiatives, epics, and slices sit inside a project just as they do in a repo
without projects. Requirements can sit at any level and bind everything beneath it.

A repo that plans one product has no projects and no `projects/` folder. Its root follows `planning:layout`, and the
rest of this file doesn't apply. A repo with projects has at least two. There is no project registry: the projects are
what `projects/` contains, and the README names each one in its Contents rows
([repository-entry.md](./repository-entry.md)).

Name a project after the product it plans, not a team, phase, or technology.

## The program root (planning:program-root)

In a repo with projects, the root holds what binds the whole program, and no work of its own. It always has:

- `README.md`, the repo's only README; projects don't get their own
- `charter/`, the program's charter ([charter.md](./charter.md))
- `projects/`, one folder per project

It may also have:

- `requirements.md` and `engineering.md`, for records that bind the whole program
- `decisions.md`, for decisions that span projects or that no project owns
- `milestones.md`, for destinations that are the program's rather than one project's, and `delivered.md` once one is
  reached
- `strategy/`, for direction-setting papers ([structure.md](./structure.md))
- `mockup-kit/`, the one kit every project's mockups share ([mockups.md](./mockups.md))
- `research/`, `presentations/`, and `supporting/`, as in a repo without projects

Every epic belongs to a project, so the root has no `work/`, `delivered/`, `epics.md`, or `initiatives.md`.

## The project folder (planning:project-folder)

A project folder is laid out like the root of a repo without projects, minus what belongs to the program: `README.md`,
`strategy/`, `mockup-kit/`, and `supporting/`.

It always has `charter/`, whose `mission.md` is the project's front door; the `epics.md`, `milestones.md`, and
`delivered.md` registries ([registries.md](./registries.md)); and `work/` and `delivered/` for its live and archived
epic and initiative folders. It may have `initiatives.md` if it uses initiatives, `requirements.md` and `engineering.md`
for records that bind every epic in the project, `decisions.md` for decisions that span its epics or that no epic owns,
and `research/` and `presentations/`.

An epic lives at `projects/<project>/work/<epic>/`, or `projects/<project>/work/<initiative>/<epic>/` under an
initiative, and moves to the same path under the project's `delivered/` when it is delivered.

## Project slugs (planning:project-slugs)

A project slug is reserved across the repo. No initiative, standalone epic, persona, job, milestone, or program-level
`product:`, `engineering:`, or `decision:` record may take it as its own slug, so an id whose first segment matches a
project slug always names that project. Like any product id, a project slug is never renamed or reused.

## Work shared across projects (planning:cross-project)

Each record lives at the narrowest level it binds: an epic or initiative, a project, or the program. A requirement,
constraint, or decision that binds more than one project, or a milestone that is no single project's destination,
belongs to the program. A capability several projects build on is a capability epic in the project that owns it
([layout.md](./layout.md)), since the program root holds no work; other projects cite it by its full id. Nothing shared
is copied into a second project. Where personas and jobs live is covered in [charter.md](./charter.md).

Moving an epic or initiative to another project, or a record from a project up to the program, changes its id
([namespaces.md](./namespaces.md)).
