# Repository entry

What a requirements repo must carry so its content reads correctly without this framework at hand. The framework
supplies none of it.

## Repository entry (planning:repository-entry)

A repo holding product or engineering content carries one README at its root, the `work/` tree of `planning:layout` in
[`./layout.md`](./layout.md) — inside each project folder when it has projects (`planning:projects` in
[`./projects.md`](./projects.md)) — and nothing that needs this framework to be read: no `AGENTS.md`, `CLAUDE.md`,
`context/`, or `winter-ext.toml`, no rule text, no `planning:` id, no tool or extension name, and no deferring to "the
framework rules". The README opens with a `#` title naming the product's requirements, such as
`# Toolshed requirements`, and directly under it, before any `##`, one paragraph naming the product and saying the repo
holds requirements content only. Its `##` sections follow, one for each `###` below, starting at Contents, all required,
in this order; Upstream schemes appears only when the repo holds engineering content. Each section holds the parts for
the tiers the repo holds, and a tier's part is omitted when the repo does not hold that tier.

Product intent lives in one of four places, and each section below that depends on it says how: in this repo; in another
repo; only in a tracker or wiki; or mixed, partly in this repo and partly elsewhere.

The README routes to `work/`, `delivered/`, and the root files, or, in a repo with projects, to each project folder and
the program's root files; no project carries a README of its own. No index file maps the tree: each folder's `epic.md`
or `initiative.md` is its front door, and the layout says what else a folder holds (`planning:layout` in
[`./layout.md`](./layout.md)).

Whatever the case, a product id has exactly one home. While the repo holds a namespace's registry, the registry row is
the home of every id in it, even one whose intent lives elsewhere: the row's id links the external home, and the
subject's intent has no file here. An epic is the exception: one planned in a tracker still has an `epic.md`, which
carries its status, names the tracker epic in `external:`, and is the home of its id and the target of its row's link
(`planning:tracker-epic` in [`./layout.md`](./layout.md)). When the repo holds no product file beyond those `epic.md`
files, the product rules do not apply to it; its `work/` folders still exist, each pointing upstream at the tracker or
the other repo. Product content cites only product ids and the external homes the README declares for them. Engineering
content conforms fully in every case; only the Upstream schemes table changes.

### Contents

- A short sentence saying the repo is organized by epic, then a `Path | What it holds` table with one plain line per
  path, and a few sentences only for what the table cannot say.
- Product's rows: `charter/`, `initiatives.md` when used, `epics.md`, `milestones.md`, `delivered.md`, `mockup-kit/`
  when present, `work/`, `delivered/`, and, written as `work/<initiative>/<epic>/…`, `initiative.md`, `epic.md`,
  `requirements.md`, and `mockups/`.
- Engineering's rows: the root `engineering.md` when present, and, written as `work/<initiative>/<epic>/…`,
  `engineering.md`, `assumptions.md`, `spec.md` or `spec/`, and `slices/`.
- A shared file such as `decisions.md` gets one row, which either tier may write.
- In a repo with projects: the program's root files, then one row per project folder, `projects/<project>/`, naming the
  product it plans — these rows are the repo's list of projects — and the folder files written as
  `projects/<project>/work/<initiative>/<epic>/…`.
- In another repo, the repo holds no product file and product has no rows; only in a tracker or wiki, it holds only each
  tracker-planned epic's `epic.md`, and that is product's one row.

### Upstream schemes

- The `Scheme | Resolves to | Example` table `planning:scheme-declaration` in [`./derivation.md`](./derivation.md) owns,
  introduced as how a reader resolves the upstream ids requirements and assumptions cite.
- Its `product:` row by case: in this repo, this repository and where an epic's product requirements are looked up; in
  another repo, that repo's URL and where they are looked up; only in a tracker or wiki, "not used", plus one row per
  tracker or wiki scheme requirements cite; mixed, both kinds of row, each requirement citing whichever scheme the
  README gives for that intent.

### Frontmatter

- For each file kind product content gives frontmatter — `epic.md`, `initiative.md`, and a requirement leaf in folder
  form — one short YAML example showing every key.
- A `Key | Meaning | Values` table or a tight list covering `epic`, `initiative`, `refinement`, `status`, `external` in
  its scalar form, and `epics`.
- One line per refinement value, `outline`, `refined`, `final`, and per epic status, `planned`, `in-progress`,
  `delivered`, saying what it means.
- The repo's format described in plain terms, citing no rule id.
- A slice's keys — `name`, `external` in its scalar form, `depends-on` with what it may name, and `code`
  (`planning:slice-files` in [`./slices.md`](./slices.md)) — in one short YAML example.
- In a repo holding no product content, the keys and values of each `epic.md` engineering keeps for an epic planned in a
  tracker (`planning:tracker-epic`): `epic`, `refinement` and its grades, `status` and its values, and `external` in its
  scalar form.

### Markers

One line per status word content puts in a body rather than frontmatter: the milestone chart statuses `planned`,
`in-progress`, `delivered` when the repo holds product content; the **Proposed.** marker on a requirement; and the
**Open.** marker and **Decider:** line on a decision.

### Ids

- A `Prefix | Names | Defined in` table, one row per product prefix, its Defined in cell naming the id's canonical home
  (`planning:id-namespaces`) by case: a path here when the namespace lives in this repo; `<repo URL> — <path>` in
  another repo; `<tracker or wiki> — <project or space>` only in a tracker or wiki; and, mixed, the registry plus every
  external system its rows link to.
- How an epic id carries its initiative, how a bare `product:` resolves, and that an id is cited as plain text and found
  by searching for the heading or row carrying it.
- In a repo with projects, how an id carries its project as its first segment, and that inside a project an id may drop
  it and resolves in the project first, then at the program.
- Rows for `engineering:` and `assume:` when the repo holds engineering content, their Defined in cell naming the file
  in each work folder and at the root that holds them, or the other repo's URL and path.
- How a scoped engineering id carries its owner's epic id, that a bare `engineering:` or `assume:` resolves from the
  citing folder outward to the root, and a link to `work/`.

**Detect.** A README missing one of these sections, or naming a rule id, an extension, or a tool.
