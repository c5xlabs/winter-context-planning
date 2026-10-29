# ❄️ winter-engineering-requirements

The **Engineering Requirements Framework**: a [winter](https://github.com/paul-gross/winter) extension of rules for the
engineering side of a requirements repo — what the system must do, why, what engineering is assuming, how it is to be
built, and in what steps.

📚 **Documentation:** <https://paul-gross.github.io/winter-docs/>

## ✨ Features

- **Requirements** — one record per `engineering:` id in the epic's `engineering.md`, each a sentence or two of what
  engineering commits to beyond the product requirements it serves, including constraints such as the language or a
  data-handling rule. A shared capability is an epic of its own, never a folder per service.
- **Derivation** — every requirement cites the product intent it serves through typed upstream ids, unless it is an
  engineering-owned constraint serving no product requirement.
- **Assumptions** — product intent engineering had to assume, in the folder's `assumptions.md`, written in product terms
  and deleted once product confirms or rejects it.
- **Specs** — the technical contracts in the folder's `spec.md` that answer its requirements, frozen once delivered.
- **Slices** — the ordered changes that build an epic, one file each in its `slices/`, derived from its requirements and
  spec and cut so the main branch stays releasable after each; the work tracker owns their progress.
- **Decisions** — `decision:` entries in each folder's shared `decisions.md`, open until the call is made; clarifying
  questions sit inline at the end of the file they concern.
- **Workflows** — [slicing an epic](./context/workflows/slice-an-epic.md) and
  [reviewing requirements](./context/workflows/requirements-review.md) against the product intent they serve.

## 🚀 Installation

Add to the workspace's `.winter/config.toml`:

```toml
[[standalone_repository]]
name = "winter-engineering-requirements"
url = "git@github.com:paul-gross/winter-engineering-requirements.git"
path = ".winter/ext/engineering-requirements"
```

Then run `winter ws init`.

## 🧩 How it works

A requirements repo is organized by product work: one folder per epic under `work/`, optionally grouped by initiative,
moving to `delivered/` once finished. This framework governs the engineering files in each folder and the engineering
entries in the files both frameworks share. It holds no content itself, and ships no skills, agents, lint, or tooling.

Engineering derives from product intent but never assumes where it is. A requirement cites upstream ids by scheme —
`product:volunteer-shifts/coordinator-cover`, `jira:SHED-412`, `assume:volunteer-shifts/cover-max-duration`, or a bare
slug, resolved outward from the citing folder — and the repo's README declares where each scheme resolves. Product
intent can live in the same repo, in another repo, in a tracker or wiki, or across several; only that table changes.

The repo never needs this framework to be read: every id appears verbatim at its home, every status is in the README
glossary, and no file names the framework or its tooling. Agents load the framework lazily, reading
[index.md](./index.md) when they work in or change an engineering-focused requirements repo, or resolve an `ereq:` rule
id.

## 🎯 Scope

The engineering side only. The framework works with or without a product framework installed: an engineering-only repo
keeps the same `work/` tree, each epic folder's `epic.md` carrying its status and pointing upstream at the tracker. The
[Product Requirements Framework](https://github.com/paul-gross/winter-product-requirements) is the optional companion
for the product side; both carry the same layout rule, so their files sit side by side in one work folder.

## 🏔️ Adopting it in a requirements repo

1. Add the README intro and the sections the framework requires — contents, upstream schemes, frontmatter, markers, ids
   ([repository-entry.md](./context/repository-entry.md)).
2. Create one folder per epic under `work/`, with an `epic.md` for an epic planned in a tracker
   ([layout.md](./context/layout.md)).
3. Write requirements, assumptions, and specs following the rules routed from [context/index.md](./context/index.md).

## 🗂️ Files

| File                                                                           | Covers                                                                                                                       |
| ------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------- |
| [index.md](./index.md)                                                         | Extension entry point; when to read the routing hub                                                                          |
| [context/index.md](./context/index.md)                                         | Agent routing hub                                                                                                            |
| [repository-entry.md](./context/repository-entry.md)                           | README sections a conforming repo carries                                                                                    |
| [namespaces.md](./context/namespaces.md)                                       | Engineering id namespaces, slugs, scopes, citation                                                                           |
| [layout.md](./context/layout.md)                                               | The shared `work/` layout, file ownership, file-or-folder, front doors, epics planned in a tracker, the `delivered/` archive |
| [structure.md](./context/structure.md)                                         | Engineering files, admission, placement, changing in place, what is deliberately absent                                      |
| [engineering.md](./context/engineering.md)                                     | Product vs engineering requirements; `engineering:` ids, record shape, constraints, recommended sections, removal            |
| [derivation.md](./context/derivation.md)                                       | What a requirement serves, upstream schemes, the scheme table                                                                |
| [assumptions.md](./context/assumptions.md)                                     | `assume:` records and their lifecycle                                                                                        |
| [specs.md](./context/specs.md)                                                 | Epic specs, shared contracts, freeze on delivery                                                                             |
| [slices.md](./context/slices.md)                                               | Slice files, how an epic is cut, slice order, re-slicing                                                                     |
| [workflows/slice-an-epic.md](./context/workflows/slice-an-epic.md)             | The steps for slicing an epic                                                                                                |
| [workflows/requirements-review.md](./context/workflows/requirements-review.md) | The steps for checking engineering content against its product requirements                                                  |
| [voice.md](./context/voice.md)                                                 | The voice engineering content is written in, and the tells it avoids                                                         |
| [decisions.md](./context/decisions.md)                                         | The bar for a decision; open and made decisions; inline clarifying questions                                                 |
| [contributing.md](./context/contributing.md)                                   | Engineering's part of the lifecycle, commit messages, checklists                                                             |

## License

Source-available under the Functional Source License 1.1 (FSL-1.1-ALv2). Each release converts to Apache License 2.0 two
years after it ships. See LICENSE.
