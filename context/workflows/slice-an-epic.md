# Slice an epic

Cut an epic into the ordered changes that build it, writing its `slices/` folder, either for the first time or after its
requirements or spec change. [`../slices.md`](../slices.md) says what a slice holds and how slices are cut; this is the
order of work.

1. **Read the sources.** In the epic folder: `epic.md`, the product requirements or upstream intent its README points
   to, `engineering.md`, `assumptions.md`, the spec, and `decisions.md`. Then the `engineering.md` of its initiative,
   project, and root, and the `epic.md` of every epic it builds on.
2. **Choose the strategy** for how the change reaches a system already in use. If the epic's constraints don't settle it
   and the choice matters, record a decision first.
3. **Cut and order the slices** (`planning:slice-cuts`, `planning:slice-order`): seam first, then each surface,
   carry-over, proof, and harness, within the strategy's sequence. Number them in build order.
4. **Fill the gaps.** A fact a slice needs that no source states goes to its home first, as an assumption, requirement,
   decision, spec section, or open question, so the slice can cite it.
5. **Write the files** (`planning:slice-files`), pointing `code:` at the code each slice changes. When re-slicing, a
   filed slice that still describes the same change keeps its name and `external:` (`planning:slice-lifecycle`).
6. **Check the cut.**
   - Every requirement, acceptance bullet, and spec section of the epic is delivered by a slice.
   - Every `depends-on` names something the slice builds on: a lower-numbered slice of this epic, or an epic or
     initiative.
   - Each slice merges alone and leaves the main branch releasable.
   - The strategy's closing step is a slice of its own.
7. **Report** the slices in order with their dependencies and every gap filled or left open, then commit
   (`planning:commit-messages` in [`../contributing.md`](../contributing.md)).
