# Planning Framework

These are the rules for what goes in a requirements repo: the files product owns, the files engineering owns, and the
files they share. Read the one row that matches your task. Each `planning:<slug>` id is defined in a heading of the file
that owns it. Rules cite these ids; the planning content itself never does.

If the request is a whole workflow, follow the workflow. It sends you to the rules it needs.

| Workflow                                                                   | When the request is                                                                     |
| -------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| [`./workflows/deliver-an-epic.md`](./workflows/deliver-an-epic.md)         | Marking an epic delivered and archiving it                                              |
| [`./workflows/slice-an-epic.md`](./workflows/slice-an-epic.md)             | Slicing or re-slicing an epic                                                           |
| [`./workflows/requirements-review.md`](./workflows/requirements-review.md) | Checking an epic's engineering content against its product requirements, before slicing |

| File                                             | When to read                                                                                                  |
| ------------------------------------------------ | ------------------------------------------------------------------------------------------------------------- |
| [`./repository-entry.md`](./repository-entry.md) | Setting up a repo's README or upstream scheme table, or product content lives in a tracker                    |
| [`./projects.md`](./projects.md)                 | Splitting a repo into projects, or placing something in a repo that has them                                  |
| [`./namespaces.md`](./namespaces.md)             | Citing or minting an id, or moving an epic between initiatives or projects                                    |
| [`./layout.md`](./layout.md)                     | Creating, moving, splitting, or archiving a work folder or its files, or keeping an epic planned in a tracker |
| [`./structure.md`](./structure.md)               | Adding, moving, renaming, or retiring a document, or adding a folder                                          |
| [`./charter.md`](./charter.md)                   | Writing mission, vision, personas, or jobs                                                                    |
| [`./registries.md`](./registries.md)             | Editing `initiatives.md`, `epics.md`, `milestones.md`, or `delivered.md`, or an epic's milestone-chart status |
| [`./intent.md`](./intent.md)                     | Writing an `epic.md` or `initiative.md`, deciding epic versus initiative, or moving an epic's status          |
| [`./requirements.md`](./requirements.md)         | Writing product requirements, or deciding whether a requirement is product's or engineering's                 |
| [`./engineering.md`](./engineering.md)           | Writing or changing an engineering requirement or constraint                                                  |
| [`./derivation.md`](./derivation.md)             | Linking an engineering requirement to the product intent it serves, or adding an upstream scheme              |
| [`./assumptions.md`](./assumptions.md)           | Engineering must assume missing product intent, or an assumption is confirmed or rejected                     |
| [`./specs.md`](./specs.md)                       | Writing an epic's technical contracts                                                                         |
| [`./slices.md`](./slices.md)                     | Writing or ordering an epic's slices, or deciding how a change reaches a system in use                        |
| [`./decisions.md`](./decisions.md)               | Recording, deferring, or making a decision, or asking a clarifying question                                   |
| [`./voice.md`](./voice.md)                       | Writing charter, registry, product-requirements, or engineering prose                                         |
| [`./mockups.md`](./mockups.md)                   | Building a mockup kit, or authoring or publishing mockups                                                     |
| [`./contributing.md`](./contributing.md)         | Taking an epic end to end, committing, or landing a change                                                    |
