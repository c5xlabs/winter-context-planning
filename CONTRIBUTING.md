# Contributing

`winter-context-planning` is a docs repo — the rules of the Planning Framework, under `context/`, routed from
[`context/index.md`](./context/index.md). The product tier is under `context/product/`, the engineering tier under
`context/engineering/`. Changes target a rule file directly. This file covers changing the framework itself; the
lifecycle and commit rules for a planning repo's content are
[`context/product/contributing.md`](./context/product/contributing.md) and
[`context/engineering/contributing.md`](./context/engineering/contributing.md).

## Shared rules

The product and engineering tiers each carry their own copy of the rules they share, wrapped in matching
`<!-- shared:<id> -->` … `<!-- /shared:<id> -->` markers. Text inside a marker must stay byte-identical to its
counterpart in the other tier, so change both in the same pass. The layout, the file-ownership principle, and the
formats of the shared files are all shared rules. Tier-specific wording — prefixes, owner names, examples — stays
outside the markers.

## Routing

[`context/index.md`](./context/index.md) routes to the two tier routers, `context/product/index.md` and
`context/engineering/index.md`: every row states *when to read* the target, never what is inside it. The root
[`index.md`](./index.md) stays a short pointer to it. Adding, moving, or removing a rule file updates its tier router
row and the README's Files table in the same change; a `planning:` rule id lives only in the heading of the rule that
defines it.

## Commit messages

[Conventional Commits](https://www.conventionalcommits.org/) with a scope:

```text
<type>(<scope>): <description>
```

- Types: `docs` is the common case; also `feat`, `fix`, `chore`, `refactor`.
- Scope: `winter-context-planning`.

## Pre-push checks

Every change, including a copyedit, passes the two markdown checks CI runs:

```bash
dprint check          # dprint fmt to apply
rumdl check .         # rumdl check . --fix for the autofixable subset
```

## Delivery

- Default branch: `master`.
- Primary contributors push directly to `master` — rebase onto the latest `origin/master` first so history stays linear.
- Outside contributors: open a PR against `master`.

Co-author agent-assisted commits per your harness's conventions.
