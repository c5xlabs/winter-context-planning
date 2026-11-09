# Planning Framework

Rules for the content of a requirements repo — product-owned files, engineering-owned files, and the files both tiers
share — follow the one row that matches your task. A cited `planning:<slug>` id is defined in the `(planning:<slug>)`
heading of the file that owns it; content never cites these ids.

When the request is a whole workflow, follow it; it routes to the rules it needs:

| Workflow                                                                   | When the request is                                                                                                         |
| -------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| [`./workflows/deliver-an-epic.md`](./workflows/deliver-an-epic.md)         | Marking an epic delivered and archiving its folder                                                                          |
| [`./workflows/slice-an-epic.md`](./workflows/slice-an-epic.md)             | Slicing an epic into the changes that build it, or re-slicing one                                                           |
| [`./workflows/requirements-review.md`](./workflows/requirements-review.md) | Checking an epic's engineering content still meets its product requirements, after product intent changes or before slicing |

| File                                             | When to read                                                                                                                                            |
| ------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [`./repository-entry.md`](./repository-entry.md) | Setting up a repo's README or its upstream scheme table, or product content lives in a tracker or wiki                                                  |
| [`./projects.md`](./projects.md)                 | Splitting a repo into projects, or placing a file, record, or shared capability in a repo that has them                                                 |
| [`./namespaces.md`](./namespaces.md)             | Before citing an id or minting one, or moving an epic into or out of an initiative or between projects                                                  |
| [`./layout.md`](./layout.md)                     | Before creating, moving, splitting, or archiving a work folder or a file in one, keeping an epic planned in a tracker, or placing shared capability     |
| [`./structure.md`](./structure.md)               | Before adding, moving, renaming, or retiring a document, or adding a folder                                                                             |
| [`./charter.md`](./charter.md)                   | Writing or changing mission, vision, personas, or jobs                                                                                                  |
| [`./registries.md`](./registries.md)             | Before editing `initiatives.md`, `epics.md`, `milestones.md`, or `delivered.md`, or moving an epic's status in a milestone chart                        |
| [`./intent.md`](./intent.md)                     | Deciding whether work is one epic or an initiative; writing an `epic.md` or an `initiative.md`, or moving an epic's status or refinement                |
| [`./requirements.md`](./requirements.md)         | Deciding whether a requirement is product's or engineering's; writing product requirements or their acceptance bullets, or splitting records into files |
| [`./engineering.md`](./engineering.md)           | Writing, changing, or removing an engineering requirement, or recording an engineering constraint                                                       |
| [`./derivation.md`](./derivation.md)             | Linking an engineering requirement to the product intent it serves, or adding an upstream scheme                                                        |
| [`./assumptions.md`](./assumptions.md)           | Product intent is missing and engineering must assume it, or an assumption is confirmed or rejected                                                     |
| [`./specs.md`](./specs.md)                       | Writing or changing an epic's technical contracts                                                                                                       |
| [`./slices.md`](./slices.md)                     | Writing, ordering, or changing an epic's slices, or deciding how a change reaches a system in use                                                       |
| [`./decisions.md`](./decisions.md)               | Before recording, deferring, or making a decision, or asking a clarifying question                                                                      |
| [`./voice.md`](./voice.md)                       | Writing charter, registry, product-requirements, or engineering prose                                                                                   |
| [`./mockups.md`](./mockups.md)                   | Building a mockup kit, authoring a mockup, or publishing mockups                                                                                        |
| [`./contributing.md`](./contributing.md)         | Taking an epic from idea to delivered, deriving and slicing its engineering content, committing, or landing a change end to end                         |
