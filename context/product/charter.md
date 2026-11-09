# Charter

A charter is the standing product direction, kept in `charter/`, along with the `persona:` and `job:` registries. The
framework doesn't supply a charter. It only governs what a charter must hold.

## Charter files (planning:charter)

A repo holding product content carries a `charter/` with these files:

- `mission.md` (required) opens with what the product is and whom it serves, then has three sections. `## Scope filter`
  is the test a proposed feature must pass to belong. `## Success criteria` lists observable outcomes, each citing the
  `persona:` and `job:` ids it concerns. `## Non-goals` lists what the product deliberately is not, and why.
- `vision.md` (optional) is prose, with theme headings if you like, describing where the product is heading in terms of
  the people it serves.
- `personas.md` (required) holds the persona registry.
- `jobs.md` (required) holds the job registry.

Every epic and milestone is judged against the scope filter, so it has to be able to reject something. Write it as a
test, not a feature list: *"A proposed feature belongs when it removes routine work from a declared job or advances a
declared milestone."*

The charter is written in the product voice ([`./voice.md`](./voice.md)). It states intent, and it points to product
requirements, research, and decisions rather than restating them.

## Program and project charters (planning:charter-levels)

There are only two places a charter can live: the root, for the program, and, in a repo with
[projects](../shared/projects.md), each project folder. Initiatives and epics have no charter content of their own;
their intent cites the charter above them. In a repo with projects, every charter needs a `mission.md`, but its other
files exist only when there is something to put in them.

The program's charter says what the whole program is for. Its scope filter decides whether a product belongs as a
project, and it holds the personas and jobs that more than one project serves. A project's charter narrows that for one
product. Its scope filter judges the project's epics and milestones, and it holds the personas and jobs only that
project serves. It never restates the program's.

Each persona and job lives in exactly one charter. Once a second project serves a project's persona or job, meaning its
mission or epics are written for that person or that work, it moves up to the program's charter under the same slug
without the project segment. The same change rewrites every citation ([moving ids](../shared/namespaces.md)). A project
that touches people it doesn't serve cites the other project's persona in full, as in `persona:platform/operator`.

## Persona registry (planning:persona-registry)

`personas.md` is a short introduction followed by one `Persona | Who they are` table with a row per persona. A persona
is a person, never a job: `persona:shift-volunteer`, not `persona:check-in-returns`.

When the detail behind the personas, such as alignment analysis or source research, outgrows one file, switch to the
[folder form](../shared/layout.md): `personas/<persona>.md` inside the charter, one file per persona and no index. Each
file opens with who the person is, followed by the detail. Epics cite that detail rather than repeating it.

If the product serves people who don't have a persona yet, name the gap in the introduction (or in `mission.md`, for the
folder form) and cite the open decision in that charter level's `decisions.md` that will settle it.

## Job registry (planning:job-registry)

`jobs.md` is a short introduction followed by one `Job | What the person is trying to accomplish` table with a row per
job. A job names an outcome the person is after, never a feature or a screen: `job:run-a-shift`, not
`job:use-pickup-list`. If a decision settled the set of jobs, the introduction cites that `decision:` record, and the
set changes only through another decision.
