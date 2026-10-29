# Contributing

`winter-engineering-requirements` is a docs repo — the rules of the Engineering Requirements Framework, under
`context/`, routed from [`context/index.md`](./context/index.md). Changes target a rule file directly. This file covers
changing the framework itself; engineering's part of a requirements repo's lifecycle and its commit rules are
[`context/contributing.md`](./context/contributing.md).

## Shared rules

This framework and the [Product Requirements Framework](https://github.com/paul-gross/winter-product-requirements) each
carry their own copy of the rules they share, wrapped in matching `<!-- shared:<id> -->` … `<!-- /shared:<id> -->`
markers. Text inside a marker must stay byte-identical to its counterpart in the other framework, so change both in the
same pass. The layout, the file-ownership principle, and the formats of the shared files are all shared rules.
Tier-specific wording — prefixes, owner names, examples — stays outside the markers.

## Routing

[`context/index.md`](./context/index.md) is the router: every row states *when to read* the target, never what is inside
it. The root [`index.md`](./index.md) stays a short pointer to it. Adding, moving, or removing a rule file updates its
`context/index.md` row and the README's Files table in the same change; an `ereq:` rule id lives only in the heading of
the rule that defines it.

## Commit messages

[Conventional Commits](https://www.conventionalcommits.org/) with a scope:

```text
<type>(<scope>): <description>
```

- Types: `docs` is the common case; also `feat`, `fix`, `chore`, `refactor`.
- Scope: `winter-engineering-requirements`.

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
