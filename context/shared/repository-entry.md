# Repository entry

A requirements repo has to read correctly without this framework at hand. This file says what it carries to do that.

## Repository entry (planning:repository-entry)

A repo holding product or engineering content carries one README at its root and the `work/` tree described in
[`./layout.md`](./layout.md), inside each project folder when it has [projects](./projects.md). It carries nothing that
needs this framework to be read: no `AGENTS.md`, `CLAUDE.md`, `context/`, or `winter-ext.toml`, no rule text or
`planning:` id, no tool or extension name, and no deferring to "the framework rules".

The README opens with a `#` title naming the product's requirements, such as `# Toolshed requirements`, then, before any
`##`, one paragraph naming the product and saying the repo holds requirements content only. The `##` sections below
follow, all required and in this order, except that Upstream schemes appears only when the repo holds engineering
content. Each section covers only the tiers the repo holds.

The README routes to `work/`, `delivered/`, and the root files, or, with projects, to each project folder and the
program's root files. No project has a README of its own, and no index file maps the tree: each folder's `epic.md` or
`initiative.md` is its front door.

Product intent lives in one of four places: in this repo, in another repo, only in a tracker or wiki, or mixed. Several
sections below change with the case.

Whatever the case, a product id has exactly one home. While the repo holds a namespace's registry, the registry row is
the home of every id in it, even one whose intent lives elsewhere: the row's id links the external home, and that
subject has no intent file here. The exception is an epic planned in a tracker, which still has an `epic.md` carrying
its status and naming the tracker epic in `external:`; that file is its id's home and its row's link target (see
[`./layout.md`](./layout.md)). A repo whose only product files are those `epic.md` files is outside the product rules,
though its `work/` folders still exist, each pointing upstream at the tracker or the other repo.

Product content cites only product ids and the external homes the README declares for them. Engineering content conforms
fully in every case; only its Upstream schemes table changes.

### Contents

A sentence saying the repo is organized by epic, then a `Path | What it holds` table with one plain line per path, and a
few sentences for whatever the table can't say.

- Product rows: `charter/`, `initiatives.md` when used, `epics.md`, `milestones.md`, `delivered.md`, `mockup-kit/` when
  present, `work/`, `delivered/`, and, written as `work/<initiative>/<epic>/…`, `initiative.md`, `epic.md`,
  `requirements.md`, and `mockups/`. With intent in another repo, product has no rows; only in a tracker or wiki, its
  one row is the tracker-planned epics' `epic.md`.
- Engineering rows: the root `engineering.md` when present, and, written as `work/<initiative>/<epic>/…`,
  `engineering.md`, `assumptions.md`, `spec.md` or `spec/`, and `slices/`.
- A shared file such as `decisions.md` gets one row.
- With projects: the program's root files, then one row per `projects/<project>/` naming the product it plans, and the
  folder files written as `projects/<project>/work/<initiative>/<epic>/…`. Those project rows are the repo's list of
  projects.

### Upstream schemes

The `Scheme | Resolves to | Example` table [`../engineering/derivation.md`](../engineering/derivation.md) defines,
introduced as how a reader resolves the upstream ids that requirements and assumptions cite. Its `product:` row depends
on where intent lives:

- In this repo: this repository, and where an epic's product requirements are found.
- In another repo: that repo's URL, and where they are found there.
- Only in a tracker or wiki: "not used", plus one row per tracker or wiki scheme that requirements cite.
- Mixed: both kinds of row, each requirement citing whichever scheme the README gives for that intent.

### Frontmatter

- One short YAML example showing every key for each product file kind with frontmatter: `epic.md`, `initiative.md`, and
  a requirement leaf in folder form.
- The keys `epic`, `initiative`, `refinement`, `status`, `external` in its scalar form, and `epics`, as a
  `Key | Meaning | Values` table or a tight list, with a line on what each refinement value (`outline`, `refined`,
  `final`) and epic status (`planned`, `in-progress`, `delivered`) means.
- The repo's format in plain terms.
- One short YAML example of a slice's keys: `name`, `external` in its scalar form, `depends-on` with what it may name,
  and `code` (see [`../engineering/slices.md`](../engineering/slices.md)).
- With no product content, the keys of each tracker-planned epic's `epic.md`: `epic`, `refinement` and its grades,
  `status` and its values, and `external` in its scalar form.

### Markers

One line per status word that sits in a body rather than frontmatter: the milestone chart statuses `planned`,
`in-progress`, and `delivered` when the repo holds product content, the **Proposed.** marker on a requirement, and the
**Open.** marker and **Decider:** line on a decision.

### Ids

- A `Prefix | Names | Defined in` table with one row per product prefix. Defined in names the id's home: a path here;
  `<repo URL> — <path>` for another repo; `<tracker or wiki> — <project or space>` for a tracker or wiki; and, when
  mixed, the registry plus every external system its rows link to.
- How an epic id carries its initiative, how a bare `product:` resolves, and that an id is cited as plain text and found
  by searching for the heading or row carrying it.
- With projects: an id's first segment is its project, and inside a project an id may drop it, resolving in the project
  first and then at the program.
- With engineering content, rows for `engineering:` and `assume:` whose Defined in names the file holding them in each
  work folder and at the root, or the other repo's URL and path.
- How a scoped engineering id carries its owner's epic id, that a bare `engineering:` or `assume:` resolves from the
  citing folder outward to the root, and a link to `work/`.
