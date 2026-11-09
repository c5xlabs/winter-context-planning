# Charter

`charter/` at the repo root, and in each project folder of a repo with projects: the standing product direction and the
`persona:` and `job:` registries. The framework does not supply a charter; it governs what one must hold.

## Charter files (planning:charter)

A repo holding product content carries `charter/` with these files; a repo with projects relaxes which are required
(`planning:charter-levels`):

| File          | R/O | Must hold                                                                                                                                                                                                                                                                                         |
| ------------- | --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `mission.md`  | R   | Opening prose on what the product is and whom it serves; then `## Scope filter`, the test a proposed feature passes to belong; `## Success criteria`, each observable and citing the `persona:` and `job:` ids it concerns; `## Non-goals`, each a thing the product deliberately is not and why. |
| `vision.md`   | O   | Prose, optionally under theme headings: the destination the product is heading toward, told through the people it serves.                                                                                                                                                                         |
| `personas.md` | R   | An introduction, then one table: the persona registry (`planning:persona-registry`); `personas/` in folder form.                                                                                                                                                                                  |
| `jobs.md`     | R   | An introduction, then one table: the job registry (`planning:job-registry`).                                                                                                                                                                                                                      |

The mission is the filter every epic and milestone is judged against, so its scope filter must reject something: *"A
proposed feature belongs when it removes routine work from a declared job or advances a declared milestone"*, not a list
of features. The charter is written in the product voice (`planning:product-voice` in [`./voice.md`](./voice.md)),
states intent, and references product requirements, research, and decisions rather than restating them.

## Program and project charters (planning:charter-levels)

A charter sits at exactly two levels: the program's at the root, and, in a repo with projects, one in each project
folder (`planning:projects` in [`./projects.md`](./projects.md)). An initiative or epic never holds charter content; its
intent cites the charter above it. In a repo with projects, each charter carries `mission.md`, and its `vision.md`,
`personas.md`, and `jobs.md` only when it has something to put in them; every persona and job lives in exactly one of
them.

- **The program's charter** states what the whole program is for: its mission's scope filter decides whether a product
  belongs as a project, and its personas and jobs are the people and work more than one project serves.
- **A project's charter** narrows the program's for one product: its mission's scope filter judges the project's epics
  and milestones, and its personas and jobs are the ones only that project serves. It never restates the program's.

A persona or job one project serves lives in that project's charter. Once a second project serves it — its mission or
its epics are written for that person or that work — it moves to the program's under its slug without the project
segment, in a change that rewrites every citation (`planning:moving-ids` in [`./namespaces.md`](./namespaces.md)); it is
never duplicated. Because no level redefines an outer one's slug (`planning:no-shadowing` in
[`./namespaces.md`](./namespaces.md)), a bare `persona:operator` inside a project names exactly one persona. A project
whose work touches people it does not serve cites another project's persona in full, `persona:platform/operator`.

**Detect.** Charter content in an initiative or epic folder; a persona or job slug defined in a project's charter and
the program's; a project's persona that a second project's mission or epics are written for.

## Persona registry (planning:persona-registry)

A charter's `personas.md` is the canonical home of every `persona:` id while it is small: a short introduction, then one
table `Persona | Who they are`, one row per persona — a person, never a job (`persona:shift-volunteer`, not
`persona:check-in-returns`). Once detail behind the personas — alignment analysis, source research — outgrows one file,
it takes the folder form (`planning:file-or-folder` in [`./layout.md`](./layout.md)): `personas/<persona>.md` inside the
charter, one leaf per persona and no index, each leaf the home of its id, opening with who the person is, then the
detail behind them. Either way the detail is not duplicated in epics. A known gap — people the product serves with no
persona yet — is named in the introduction, or in folder form in `mission.md`, citing the open decision in the
`decisions.md` at the charter's level that will settle it.

## Job registry (planning:job-registry)

A charter's `jobs.md` is the canonical home of every `job:` id at its level: a short introduction, then one table
`Job | What the person is trying to accomplish`, one row per job. A job names an outcome a person pursues, never a
feature or screen (`job:run-a-shift`, not `job:use-pickup-list`). When a decision settled the job set, the introduction
cites that `decision:` record, and the set changes only through one.
