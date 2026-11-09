# ❄️ winter-context-planning

The **Planning Framework**: a [winter](https://github.com/paul-gross/winter) extension of rules for a planning repo, in
two tiers. The **product tier** covers the charter, personas and jobs, initiatives, epics and milestones, product
requirements, product decisions, and mockups, so product intent stays findable, citable, and readable by anyone who
opens the repo. The **engineering tier** covers what the system must do, why, what engineering is assuming, how it is to
be built, and in what steps.

It merges the former Product Requirements Framework (`winter-product-requirements`) and Engineering Requirements
Framework (`winter-engineering-requirements`); both histories are kept, and their rules now share one `planning:` id
namespace.

📚 **Documentation:** <https://paul-gross.github.io/winter-docs/>

## ✨ Features

### Product tier

- **Charter** — mission, vision, and the persona and job registries every epic answers to.
- **Projects** — an optional level that splits one program into several products, each with its own charter, registries,
  and work, under a program root holding what binds them all.
- **Epics and initiatives** — one folder per epic under `work/`, optionally grouped by initiative, with the registries
  that list them and a `delivered/` archive once they finish.
- **Product requirements** — one record per `product:` id, each with acceptance bullets, kept apart from what
  engineering commits to.
- **Stable, citable ids** — `persona:`, `job:`, `initiative:`, `epic:`, `product:`, `milestone:`, and `decision:` ids
  built from slugs, never numbers, each with one canonical home.
- **Decisions** — open until the call is made, with clarifying questions inline at the end of the file they concern.
- **Mockups** — the kit a repo supplies, how mockups are authored, and how they are published.
- **Product voice** — the voice product intent is written in, and the tells it avoids.
- **Delivering an epic** — a workflow for marking an epic delivered and archiving its folder.

### Engineering tier

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
name = "winter-context-planning"
url = "git@github.com:c5xlabs/winter-context-planning.git"
path = ".winter/ext/planning"
```

Then run `winter ws init`.

## 🧩 How it works

A requirements repo holds content only, organized by product work: one folder per epic under `work/`, optionally grouped
by initiative, moving to `delivered/` once finished, with program-wide files at the root; a program of several products
splits into project folders, each laid out the same way. The framework governs the product-owned files — the charter,
the registries, each folder's `epic.md` or `initiative.md`, `requirements.md`, and `mockups/` — the engineering-owned
files — `engineering.md`, `assumptions.md`, `spec.md`, and `slices/` — and the files both tiers share, such as
`decisions.md`: what each holds, how ids are minted and kept stable, how decisions are recorded open or made, where
clarifying questions sit, and the voice each tier is written in. Where the framework cannot supply something — a README,
a charter, a mockup kit — it states what the repo's own version must contain.

Engineering derives from product intent but never assumes where it is. A requirement cites upstream ids by scheme —
`product:volunteer-shifts/coordinator-cover`, `jira:SHED-412`, `assume:volunteer-shifts/cover-max-duration`, or a bare
slug, resolved outward from the citing folder — and the repo's README declares where each scheme resolves. Product
intent can live in the same repo, in another repo, in a tracker or wiki, or across several; only that table changes.
Citation runs one way: product files never cite engineering ids.

The framework stays out of the content. A conforming repo carries no rule text, agent instructions, or tooling
references; every id appears verbatim at its home and every status is in the README glossary, so the content reads
correctly without this repo at hand. The framework holds no content itself, and ships no skills, agents, lint, or
tooling.

Agents working in the workspace load the framework on demand through [`index.md`](./index.md) and cite its rules as
`planning:<slug>`.

## 🎯 Scope

Both sides of a requirements repo, product and engineering. Each tier stands alone: a repo may hold only product
content, only engineering content, or both, and their files sit side by side in one work folder.

## 🏔️ Adopting it in a requirements repo

1. Add the README intro and the sections [`repository-entry.md`](./context/repository-entry.md) requires for the tiers
   the repo holds.
2. For product content, add the required root files — `charter/`, `epics.md`, `milestones.md`, `delivered.md` — and a
   folder under `work/` per epic, with its `epic.md`, in the change that names the epic, following the lifecycle in
   [`contributing.md`](./context/contributing.md). For engineering content alone, create one folder per epic under
   `work/`, with an `epic.md` for an epic planned in a tracker ([`layout.md`](./context/layout.md)).
3. Write requirements, assumptions, specs, and slices following the rules routed from
   [`context/index.md`](./context/index.md).

## 🗂️ Files

| File                                                                             | Covers                                                                                                                |
| -------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| [`index.md`](./index.md)                                                         | Extension entry point; when to read the routing hub                                                                   |
| [`context/index.md`](./context/index.md)                                         | Agent routing hub                                                                                                     |
| [`repository-entry.md`](./context/repository-entry.md)                           | The README sections a repo must carry, by tier; external homes                                                        |
| [`projects.md`](./context/projects.md)                                           | The project level: program root, project folders, reserved slugs, work shared across projects                         |
| [`namespaces.md`](./context/namespaces.md)                                       | Id prefixes of both tiers, slugs, stability, scopes, citation, and the engineering ids product never cites            |
| [`layout.md`](./context/layout.md)                                               | The `work/` layout, file ownership, file-or-folder, front doors, epics planned in a tracker, the `delivered/` archive |
| [`structure.md`](./context/structure.md)                                         | Product and engineering areas, admission, placement, changing in place, what is deliberately absent                   |
| [`charter.md`](./context/charter.md)                                             | Mission, vision, persona and job registries                                                                           |
| [`registries.md`](./context/registries.md)                                       | Shapes of `initiatives.md`, `epics.md`, `milestones.md`, `delivered.md`                                               |
| [`intent.md`](./context/intent.md)                                               | Epic or initiative; `epic.md` and `initiative.md`, their frontmatter, epic status and refinement, sections            |
| [`requirements.md`](./context/requirements.md)                                   | Classifying a requirement; product requirement records, acceptance, requirement files                                 |
| [`engineering.md`](./context/engineering.md)                                     | `engineering:` ids, record shape, constraints, recommended sections, removal                                          |
| [`derivation.md`](./context/derivation.md)                                       | What a requirement serves, upstream schemes, the scheme table                                                         |
| [`assumptions.md`](./context/assumptions.md)                                     | `assume:` records and their lifecycle                                                                                 |
| [`specs.md`](./context/specs.md)                                                 | Epic specs, shared contracts, freeze on delivery                                                                      |
| [`slices.md`](./context/slices.md)                                               | Slice files, how an epic is cut, slice order, re-slicing                                                              |
| [`decisions.md`](./context/decisions.md)                                         | The bar for a decision; open and made decisions; inline clarifying questions                                          |
| [`voice.md`](./context/voice.md)                                                 | The product and engineering voices, and the tells each avoids                                                         |
| [`mockups.md`](./context/mockups.md)                                             | Mockup kit, authoring, publishing                                                                                     |
| [`contributing.md`](./context/contributing.md)                                   | The lifecycle from idea to delivered, engineering's part of it, commit messages, checklists                           |
| [`workflows/deliver-an-epic.md`](./context/workflows/deliver-an-epic.md)         | The steps for delivering and archiving an epic                                                                        |
| [`workflows/slice-an-epic.md`](./context/workflows/slice-an-epic.md)             | The steps for slicing an epic                                                                                         |
| [`workflows/requirements-review.md`](./context/workflows/requirements-review.md) | The steps for checking engineering content against its product requirements                                           |

## License

Source-available under the Functional Source License 1.1 (FSL-1.1-ALv2). Each release converts to Apache License 2.0 two
years after it ships. See LICENSE.
