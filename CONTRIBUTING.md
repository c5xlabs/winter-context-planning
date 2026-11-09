# Contributing

`winter-context-planning` is a docs repo — the rules of the Planning Framework, under `context/`, routed from
[`context/index.md`](./context/index.md). Changes target a rule file directly. This file covers changing the framework
itself; the lifecycle and commit rules for a requirements repo's content are
[`context/contributing.md`](./context/contributing.md).

## Routing

[`context/index.md`](./context/index.md) is the router: every row states *when to read* the target, never what is inside
it. The root [`index.md`](./index.md) stays a short pointer to it. Adding, moving, or removing a rule file updates its
`context/index.md` row and the README's Files table in the same change; a `planning:` rule id lives only in the heading
of the rule that defines it, and no two rules share a slug.

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
