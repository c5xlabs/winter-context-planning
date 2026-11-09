# Repository entry

How a requirements repo declares its product content, so the content reads correctly without this framework at hand.

## Repository entry (preq:repository-entry)

The framework does not supply a README; a repo holding product content carries one. It opens with a `#` title naming the
product's requirements, such as `# Toolshed requirements`, and directly under it, before any `##`, one paragraph naming
the product and saying the repo holds requirements content only. Its `##` sections follow, one for each `###` below,
starting at Contents, all required, in this order. The intro and each section state facts about the repo itself, never
about this framework or its tooling: no `preq:` id, extension name, or tool name, and no deferring to "the framework
rules". This rule owns only the product parts of the README; a section for a tier the repo does not hold is omitted.

<!-- shared:product-intent-cases -->

Product intent lives in one of four places, and each section below that depends on it says how: in this repo; in another
repo; only in a tracker or wiki; or mixed, partly in this repo and partly elsewhere.

<!-- /shared:product-intent-cases -->

The README routes to `work/`, `delivered/`, and the root files. No index file maps the tree: each folder's `epic.md` or
`initiative.md` is its front door, and the layout says what else a folder holds (`preq:layout` in
[`./layout.md`](./layout.md)).

Whatever the case, a product id has exactly one home. While the repo holds a namespace's registry, the registry row is
the home of every id in it, even one whose intent lives elsewhere: the row's id links the external home, and the
subject's intent has no file here. An epic is the exception: one planned in a tracker still has an `epic.md`, which
carries its status, names the tracker epic in `external:`, and is the home of its id and the target of its row's link
(`preq:tracker-epic` in [`./layout.md`](./layout.md)). When the repo holds no product file beyond those `epic.md` files,
this framework does not apply to it; its `work/` folders still exist, each pointing upstream at the tracker or the other
repo. Product content cites only product ids and the external homes the README declares for them.

### Contents

- A short sentence saying the repo is organized by epic, then a `Path | What it holds` table with one plain line per
  path, and a few sentences only for what the table cannot say.
- Product's rows: `charter/`, `initiatives.md` when used, `epics.md`, `milestones.md`, `delivered.md`, `mockup-kit/`
  when present, `work/`, `delivered/`, and, written as `work/<initiative>/<epic>/…`, `initiative.md`, `epic.md`,
  `requirements.md`, and `mockups/`.
- A shared file such as `decisions.md` gets one row, which either tier may write.
- In another repo, the repo holds no product file and product has no rows; only in a tracker or wiki, it holds only each
  tracker-planned epic's `epic.md`, and that is product's one row.

### Frontmatter

- For each file kind product content gives frontmatter — `epic.md`, `initiative.md`, and a requirement leaf in folder
  form — one short YAML example showing every key.
- A `Key | Meaning | Values` table or a tight list covering `epic`, `initiative`, `refinement`, `status`, `external` in
  its scalar form, and `epics`.
- One line per refinement value, `outline`, `refined`, `final`, and per epic status, `planned`, `in-progress`,
  `delivered`, saying what it means.
- The repo's format described in plain terms, citing no rule id.

### Markers

One line per status word product content puts in a body rather than frontmatter: the milestone chart statuses `planned`,
`in-progress`, `delivered`; the **Proposed.** marker on a requirement; and the **Open.** marker and **Decider:** line on
a decision.

### Ids

- A `Prefix | Names | Defined in` table, one row per product prefix, its Defined in cell naming the id's canonical home
  (`preq:id-namespaces`) by case: a path here when the namespace lives in this repo; `<repo URL> — <path>` in another
  repo; `<tracker or wiki> — <project or space>` only in a tracker or wiki; and, mixed, the registry plus every external
  system its rows link to.
- How an epic id carries its initiative, how a bare `product:` resolves, and that an id is cited as plain text and found
  by searching for the heading or row carrying it.

**Detect.** A README missing one of these sections, or naming a rule id, an extension, or a tool.
