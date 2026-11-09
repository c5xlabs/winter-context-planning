# Planning Framework

Rules for a planning repo, in two tiers. Each tier has its own router; follow the one that matches your task, or both
when a task touches product and engineering content. A cited `preq:<slug>` id is defined in the product tier, an
`ereq:<slug>` id in the engineering tier.

| Tier                                               | When to read                                                                                                          |
| -------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| [`./product/index.md`](./product/index.md)         | Product content — charter, registries, `epic.md` and `initiative.md`, product requirements, mockups — or a `preq:` id |
| [`./engineering/index.md`](./engineering/index.md) | Engineering content — engineering requirements, derivation, assumptions, specs, slices — or an `ereq:` id             |
