# ❄️ winter-context-planning

The **Planning Framework**: a [winter](https://github.com/paul-gross/winter) extension of rules for a planning repo, in
two tiers. The **product tier** covers the charter, personas and jobs, initiatives, epics and milestones, product
requirements, product decisions, and mockups, so product intent stays findable, citable, and readable by anyone who
opens the repo. The **engineering tier** covers what the system must do, why, what engineering is assuming, how it is to
be built, and in what steps.

It merges the former Product Requirements Framework (`winter-product-requirements`) and Engineering Requirements
Framework (`winter-engineering-requirements`); both histories are kept.

📚 **Documentation:** <https://paul-gross.github.io/winter-docs/>

## ✨ Features

### Product tier

- **Charter** — mission, vision, and the persona and job registries every epic answers to.
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
- **Workflows** — [slicing an epic](./context/engineering/workflows/slice-an-epic.md) and
  [reviewing requirements](./context/engineering/workflows/requirements-review.md) against the product intent they
  serve.

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

### Product tier

A requirements repo holds content only, organized by product work: one folder per epic under `work/`, optionally grouped
by initiative, moving to `delivered/` once finished, with program-wide files at the root. This framework governs the
product-owned files — the charter, the registries, each folder's `epic.md` or `initiative.md`, `requirements.md`, and
`mockups/` — and the product entries in the files both frameworks share: what each holds, how product ids are minted and
kept stable, how decisions are recorded open or made, where clarifying questions sit, and the voice product intent is
written in. Where the framework cannot supply something — a README, a charter, a mockup kit — it states what the repo's
own version must contain.

The framework stays out of the content. A conforming repo carries no rule text, agent instructions, or tooling
references; its README explains its own ids and statuses, so the content reads correctly without this repo at hand.

Product intent does not have to live in git. A repo may keep some or all of it in a work tracker or wiki and declare
where each kind of id lives; the framework then governs only the product files the repo holds.

Agents working in the workspace load the framework on demand through [`index.md`](./index.md) and cite its rules as
`preq:<slug>`.

### Engineering tier

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

Both sides of a planning repo, as two tiers. Each tier stands alone: a repo may hold only product content, only
engineering content, or both. Both carry the same layout rule, so their files sit side by side in one work folder.

## 🏔️ Adopting it in a planning repo

### Product content

1. In the planning repo, add the README sections that [`repository-entry.md`](./context/product/repository-entry.md)
   requires.
2. Add the required root files — `charter/`, `epics.md`, `milestones.md`, `delivered.md` — and a folder under `work/`
   per epic, with its `epic.md`, in the change that names the epic, following the lifecycle in
   [`contributing.md`](./context/product/contributing.md).

### Engineering content

1. Add the README intro and the sections the framework requires — contents, upstream schemes, frontmatter, markers, ids
   ([repository-entry.md](./context/engineering/repository-entry.md)).
2. Create one folder per epic under `work/`, with an `epic.md` for an epic planned in a tracker
   ([layout.md](./context/engineering/layout.md)).
3. Write requirements, assumptions, and specs following the rules routed from
   [context/engineering/index.md](./context/engineering/index.md).

## 🗂️ Files

| File                                                                                                     | Covers                                                                                                                       |
| -------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| [`index.md`](./index.md)                                                                                 | Extension entry point; when to read the routing hub                                                                          |
| [`context/index.md`](./context/index.md)                                                                 | Agent routing hub: which tier to read                                                                                        |
| [`product/context/product/index.md`](./context/product/index.md)                                         | Product tier routing hub                                                                                                     |
| [`engineering/context/engineering/index.md`](./context/engineering/index.md)                             | Engineering tier routing hub                                                                                                 |
| [`product/repository-entry.md`](./context/product/repository-entry.md)                                   | The README sections a repo must carry; external homes                                                                        |
| [`product/namespaces.md`](./context/product/namespaces.md)                                               | Product id prefixes, slugs, stability, scopes, citation, and the engineering ids product never cites                         |
| [`product/layout.md`](./context/product/layout.md)                                                       | The shared `work/` layout, file ownership, file-or-folder, front doors, epics planned in a tracker, the `delivered/` archive |
| [`product/structure.md`](./context/product/structure.md)                                                 | Product areas, admission, placement, changing in place, what is deliberately absent                                          |
| [`product/charter.md`](./context/product/charter.md)                                                     | Mission, vision, persona and job registries                                                                                  |
| [`product/registries.md`](./context/product/registries.md)                                               | Shapes of `initiatives.md`, `epics.md`, `milestones.md`, `delivered.md`                                                      |
| [`product/intent.md`](./context/product/intent.md)                                                       | Epic or initiative; `epic.md` and `initiative.md`, their frontmatter, epic status and refinement, sections                   |
| [`product/requirements.md`](./context/product/requirements.md)                                           | Product vs engineering requirements; requirement records, acceptance, requirement files                                      |
| [`product/decisions.md`](./context/product/decisions.md)                                                 | The bar for a decision; open and made decisions; inline clarifying questions                                                 |
| [`product/voice.md`](./context/product/voice.md)                                                         | The voice product intent is written in, and the tells it avoids                                                              |
| [`product/mockups.md`](./context/product/mockups.md)                                                     | Mockup kit, authoring, publishing                                                                                            |
| [`product/contributing.md`](./context/product/contributing.md)                                           | The lifecycle from idea to delivered, commit messages, checklists                                                            |
| [`product/workflows/deliver-an-epic.md`](./context/product/workflows/deliver-an-epic.md)                 | The steps for delivering and archiving an epic                                                                               |
| [`engineering/repository-entry.md`](./context/engineering/repository-entry.md)                           | README sections a conforming repo carries                                                                                    |
| [`engineering/namespaces.md`](./context/engineering/namespaces.md)                                       | Engineering id namespaces, slugs, scopes, citation                                                                           |
| [`engineering/layout.md`](./context/engineering/layout.md)                                               | The shared `work/` layout, file ownership, file-or-folder, front doors, epics planned in a tracker, the `delivered/` archive |
| [`engineering/structure.md`](./context/engineering/structure.md)                                         | Engineering files, admission, placement, changing in place, what is deliberately absent                                      |
| [`engineering/engineering.md`](./context/engineering/engineering.md)                                     | Product vs engineering requirements; `engineering:` ids, record shape, constraints, recommended sections, removal            |
| [`engineering/derivation.md`](./context/engineering/derivation.md)                                       | What a requirement serves, upstream schemes, the scheme table                                                                |
| [`engineering/assumptions.md`](./context/engineering/assumptions.md)                                     | `assume:` records and their lifecycle                                                                                        |
| [`engineering/specs.md`](./context/engineering/specs.md)                                                 | Epic specs, shared contracts, freeze on delivery                                                                             |
| [`engineering/slices.md`](./context/engineering/slices.md)                                               | Slice files, how an epic is cut, slice order, re-slicing                                                                     |
| [`engineering/workflows/slice-an-epic.md`](./context/engineering/workflows/slice-an-epic.md)             | The steps for slicing an epic                                                                                                |
| [`engineering/workflows/requirements-review.md`](./context/engineering/workflows/requirements-review.md) | The steps for checking engineering content against its product requirements                                                  |
| [`engineering/voice.md`](./context/engineering/voice.md)                                                 | The voice engineering content is written in, and the tells it avoids                                                         |
| [`engineering/decisions.md`](./context/engineering/decisions.md)                                         | The bar for a decision; open and made decisions; inline clarifying questions                                                 |
| [`engineering/contributing.md`](./context/engineering/contributing.md)                                   | Engineering's part of the lifecycle, commit messages, checklists                                                             |

## License

Source-available under the Functional Source License 1.1 (FSL-1.1-ALv2). Each release converts to Apache License 2.0 two
years after it ships. See LICENSE.
