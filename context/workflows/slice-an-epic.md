# Slice an epic

Cut an epic into the ordered changes that build it, writing its `slices/` folder. Use it to slice an epic for the first
time or to re-slice one after its requirements or spec change. What a slice holds and how slices are cut is
[`../slices.md`](../slices.md); this is only the order of work.

1. **Read the sources.** The epic folder's `epic.md`, its product requirements or the upstream intent its README points
   to, `engineering.md`, `assumptions.md`, the spec, and `decisions.md`; then the `engineering.md` of its initiative and
   of the root, and the `epic.md` of every epic it builds on.
2. **Choose the strategy.** From the constraints that bind the epic, pick how the change reaches a system already in use
   — `planning:slice-cuts`. If none settles it and the choice matters, record a decision first.
3. **Cut and order.** Seam first, then each surface, carry-over, proof, and harness, inside the strategy's sequence —
   `planning:slice-cuts`; number them in build order with dependencies pointing back — `planning:slice-order`.
4. **Fill the gaps at their homes.** Every fact a slice needs that no source states goes to its home before the slice
   cites it: an assumption, a requirement, a decision, a spec section, or an open question — `planning:slice-files`.
5. **Write the files**, pointing `code:` at the code each slice changes — `planning:slice-files`. When re-slicing, keep
   each filed slice's name and `external:` while it still describes the same change — `planning:slice-lifecycle`.
6. **Check the cut.**
   - Every requirement the epic holds, and each of its acceptance bullets, is delivered by a slice, and every spec
     section is built by one.
   - Every `depends-on` names a lower-numbered slice of this epic, or an epic or initiative, and only something the
     slice builds on.
   - Each slice is one change that merges alone and leaves the main branch releasable.
   - The strategy's closing step is a slice of its own.
   - Nothing in a slice lacks a home it cites.
7. **Report** the slices in order with what each depends on, and every gap filled or left open, then commit —
   `planning:commit-messages` in [`../contributing.md`](../contributing.md).
