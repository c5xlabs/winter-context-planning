# Charter

`charter/` at the repo root: the standing product direction and the `persona:` and `job:` registries. The framework does
not supply a charter; it governs what one must hold.

## Charter files (preq:charter)

A repo holding product content carries `charter/` with these files:

| File          | R/O | Must hold                                                                                                                                                                                                                                                                                         |
| ------------- | --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `mission.md`  | R   | Opening prose on what the product is and whom it serves; then `## Scope filter`, the test a proposed feature passes to belong; `## Success criteria`, each observable and citing the `persona:` and `job:` ids it concerns; `## Non-goals`, each a thing the product deliberately is not and why. |
| `vision.md`   | O   | Prose, optionally under theme headings: the destination the product is heading toward, told through the people it serves.                                                                                                                                                                         |
| `personas.md` | R   | An introduction, then one table: the persona registry (`preq:persona-registry`); `personas/` in folder form.                                                                                                                                                                                      |
| `jobs.md`     | R   | An introduction, then one table: the job registry (`preq:job-registry`).                                                                                                                                                                                                                          |

The mission is the filter every epic and milestone is judged against, so its scope filter must reject something: *"A
proposed feature belongs when it removes routine work from a declared job or advances a declared milestone"*, not a list
of features. The charter is written in the product voice (`preq:product-voice` in [`./voice.md`](./voice.md)), states
intent, and references product requirements, research, and decisions rather than restating them.

## Persona registry (preq:persona-registry)

`charter/personas.md` is the canonical home of every `persona:` id while it is small: a short introduction, then one
table `Persona | Who they are`, one row per persona — a person, never a job (`persona:shift-volunteer`, not
`persona:check-in-returns`). Once detail behind the personas — alignment analysis, source research — outgrows one file,
it takes the folder form (`preq:file-or-folder` in [`./layout.md`](./layout.md)): `charter/personas/<persona>.md`, one
leaf per persona and no index, each leaf the home of its id, opening with who the person is, then the detail behind
them. Either way the detail is not duplicated in epics. A known gap — people the product serves with no persona yet — is
named in the introduction, or in folder form in `mission.md`, citing the open decision in the root `decisions.md` that
will settle it.

## Job registry (preq:job-registry)

`charter/jobs.md` is the canonical home of every `job:` id: a short introduction, then one table
`Job | What the person is trying to accomplish`, one row per job. A job names an outcome a person pursues, never a
feature or screen (`job:run-a-shift`, not `job:use-pickup-list`). When a decision settled the job set, the introduction
cites that `decision:` record, and the set changes only through one.
