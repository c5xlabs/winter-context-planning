# Contributing

`winter-context-planning` holds the rules of the Planning Framework, under `context/`. This file is about changing the
framework itself. The rules for a requirements repo's own content are in
[`context/contributing.md`](./context/contributing.md).

## Routing

[`context/index.md`](./context/index.md) routes to every rule file. Each row says when to read the file, not what it
contains. The root [`index.md`](./index.md) is only a short pointer to it.

When you add, move, or remove a rule file, update its row there and the README's Files table in the same change. A
`planning:` rule id appears only in the heading of the rule that defines it, and every slug is unique.

## Commit messages

[Conventional Commits](https://www.conventionalcommits.org/) with the scope `winter-context-planning`. The type is
usually `docs`; `feat`, `fix`, `chore`, and `refactor` also apply.

```text
docs(winter-context-planning): <description>
```

Co-author agent-assisted commits the way your harness does.

## Pre-push checks

Every change, copyedits included, passes the two markdown checks CI runs:

```bash
dprint check          # dprint fmt to apply
rumdl check .         # rumdl check . --fix for the autofixable subset
```

## Delivery

Primary contributors rebase onto the latest `origin/master` and push directly to `master`. Outside contributors open a
PR against `master`.
