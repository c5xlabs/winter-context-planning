# Engineering Requirements Framework

Rules for engineering content in a requirements repo — the engineering-owned files and engineering entries in shared
files — follow the row that matches your task. A cited `ereq:<slug>` id is defined in the `(ereq:<slug>)` heading of the
file that owns it; content never cites these ids.

When the request is a whole workflow, follow it; it routes to the rules it needs:

| Workflow                                                               | When the request is                                                                                                         |
| ---------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| [workflows/slice-an-epic.md](./workflows/slice-an-epic.md)             | Slicing an epic into the changes that build it, or re-slicing one                                                           |
| [workflows/requirements-review.md](./workflows/requirements-review.md) | Checking an epic's engineering content still meets its product requirements, after product intent changes or before slicing |

| File                                         | When to read                                                                                                                                        |
| -------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| [repository-entry.md](./repository-entry.md) | Setting up a repo's engineering content or its upstream scheme table                                                                                |
| [namespaces.md](./namespaces.md)             | Before citing an engineering id or minting one, or moving an epic into or out of an initiative                                                      |
| [layout.md](./layout.md)                     | Before creating, moving, splitting, or archiving a work folder or a file in one, keeping an epic planned in a tracker, or placing shared capability |
| [structure.md](./structure.md)               | Before adding, moving, renaming, or retiring an engineering document, or adding a folder                                                            |
| [engineering.md](./engineering.md)           | Deciding whether a requirement is product's or engineering's; writing, changing, or removing one, or recording an engineering constraint            |
| [derivation.md](./derivation.md)             | Linking a requirement to the product intent it serves, or adding an upstream scheme                                                                 |
| [assumptions.md](./assumptions.md)           | Product intent is missing and engineering must assume it, or an assumption is confirmed or rejected                                                 |
| [specs.md](./specs.md)                       | Writing or changing an epic's technical contracts                                                                                                   |
| [slices.md](./slices.md)                     | Writing, ordering, or changing an epic's slices, or deciding how a change reaches a system in use                                                   |
| [voice.md](./voice.md)                       | Writing engineering requirements, specs, assumptions, or decisions                                                                                  |
| [decisions.md](./decisions.md)               | Before recording, deferring, or making an engineering decision, or asking a clarifying question                                                     |
| [contributing.md](./contributing.md)         | Deriving and delivering an epic's engineering content, committing, or landing an engineering change end to end                                      |
