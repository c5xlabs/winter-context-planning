# Planning Framework

These are the rules for what goes in a requirements repo. Product and engineering each own their files and share the
rest; a repo may hold either tier or both. Read the one row that matches your task. Each `planning:<slug>` id is defined
in a heading of the file that owns it, and each folder's index lists the ids its files define. Rules cite these ids; the
planning content itself never does.

If the request is a whole workflow, follow the workflow. It sends you to the rules it needs.

| Workflow                                                                   | When the request is                                                                     |
| -------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| [`./workflows/deliver-an-epic.md`](./workflows/deliver-an-epic.md)         | Marking an epic delivered and archiving it                                              |
| [`./workflows/slice-an-epic.md`](./workflows/slice-an-epic.md)             | Slicing or re-slicing an epic                                                           |
| [`./workflows/requirements-review.md`](./workflows/requirements-review.md) | Checking an epic's engineering content against its product requirements, before slicing |

| File                                               | When to read                                                                                                     | Rule ids                                                                                                       |
| -------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| [`./shared/index.md`](./shared/index.md)           | Laying out a repo or its folders, working with ids or projects, or recording a decision; any task in either tier | In its index                                                                                                   |
| [`./product/index.md`](./product/index.md)         | Writing or changing product content: charter, registries, epics, initiatives, product requirements, mockups      | In its index                                                                                                   |
| [`./engineering/index.md`](./engineering/index.md) | Writing or changing engineering content: requirements, assumptions, specs, slices                                | In its index                                                                                                   |
| [`./contributing.md`](./contributing.md)           | Taking an epic end to end, committing, or landing a change                                                       | `planning:lifecycle` · `planning:engineering-lifecycle` · `planning:commit-messages` · `planning:contributing` |
