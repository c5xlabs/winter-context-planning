# Review requirements

Check that an epic's engineering content still meets its product requirements, reading each side against the other, and
fix what no longer holds. Run it whenever product intent changes (a requirement added, rewritten, accepted, or deleted,
an assumption confirmed or rejected, a decision made) and before slicing or re-slicing an epic. A delivered epic is
frozen, so it isn't reviewed.

This file is only the order of work. What each record holds is in [engineering](../engineering/requirements.md),
[derivation](../engineering/derivation.md), [assumptions](../engineering/assumptions.md),
[specs](../engineering/specs.md), and [slices](../engineering/slices.md).

1. **Read both sides.** On the product side, the epic's `epic.md` and its product requirements, or the upstream intent
   the repo README's Upstream schemes table points to. On the engineering side, its `engineering.md`, `assumptions.md`,
   spec, `decisions.md`, and `slices/`, plus the `engineering.md` of its initiative, its project, and the root.
   `git log` on the product files since the engineering files last changed shows what moved.
2. **Product against engineering.** For each product requirement and each of its acceptance bullets:
   - Where engineering must commit to more than the product text says, an engineering requirement does so, and none
     merely restates the product.
   - Intent that engineering needs but product hasn't stated is an assumption, not a choice made quietly in a
     requirement or the spec.
   - At least one slice delivers it.
3. **Engineering against product.** For each engineering requirement, assumption, spec section, and slice:
   - Every upstream id it cites still exists and still says what it relied on.
   - A requirement that serves no live intent and isn't a standalone constraint is deleted.
   - A bound still keeps the promise it derives from; a latency, say, still fits the time product allows.
   - An assumption product has since stated or refused is settled.
   - A slice still derives from what it cites.
4. **Fix each record where it lives.** Rewrite or delete each engineering record that no longer holds, and fix every
   citation of an id it removes in the same change. A product requirement whose meaning is unclear gets a bullet under
   `## Open questions` in its own file, citing no engineering id; one that needs a choice gets an open decision. If any
   slice changed, re-slice with [slice an epic](./slice-an-epic.md).
5. **Report** what changed on each side and every question or decision left open, then commit as
   [contributing](../contributing.md) describes.
