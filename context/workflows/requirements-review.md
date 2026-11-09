# Review requirements

Check that an epic's engineering content still meets its product requirements, reading each side against the other, and
fix what no longer holds. Use it after product intent changes — a requirement added, rewritten, accepted, or deleted, an
assumption confirmed or rejected, a decision made — and before slicing or re-slicing an epic. A delivered epic is frozen
and is not reviewed. What each record holds is [`../engineering.md`](../engineering.md),
[`../derivation.md`](../derivation.md), [`../assumptions.md`](../assumptions.md), [`../specs.md`](../specs.md), and
[`../slices.md`](../slices.md); this is only the order of work.

1. **Read both sides.** The epic folder's `epic.md` and its product requirements, or the upstream intent its README
   points to; its `engineering.md`, `assumptions.md`, spec, `decisions.md`, and `slices/`; then the `engineering.md` of
   its initiative, its project, and the root. `git log` on the product files since the engineering files last changed
   shows what moved.
2. **Product against engineering.** For each product requirement, and each acceptance bullet under it:
   - Where engineering must commit to more than the product text says, an engineering requirement does, and none merely
     restates it — `planning:beyond-product`.
   - Intent engineering needs and product has not stated is an assumption, never a choice made silently in a requirement
     or the spec — `planning:assumption-record`.
   - At least one slice delivers it — `planning:slice-cuts`.
3. **Engineering against product.** For each engineering requirement, assumption, spec section, and slice:
   - Every upstream id it cites still exists and still says what it relied on — `planning:serves`.
   - A requirement serves live intent or is a standalone constraint; one serving nothing is deleted —
     `planning:requirement-removal`.
   - A bound still keeps the promise it derives from, such as a latency that still fits the time product gives —
     `planning:classify-requirement`.
   - An assumption product has since stated or refused is settled — `planning:assumption-lifecycle`.
   - A slice still derives from what it cites — `planning:slice-files`.
4. **Fix at the home.** Rewrite in place or delete each engineering record that no longer holds, fixing every citation
   of an id it removes in the same change — `planning:change-in-place`. A product requirement whose meaning is unclear
   gets a bullet in the `## Open questions` of its file, citing no engineering id; one that needs a choice gets an open
   decision — `planning:inline-questions`, `planning:decision-format`. When any slice changed, re-slice —
   [`./slice-an-epic.md`](./slice-an-epic.md).
5. **Report** what changed on each side and every question or decision left open, then commit —
   `planning:commit-messages` in [`../contributing.md`](../contributing.md).
