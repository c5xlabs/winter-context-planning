# Repository entry

What a requirements repo holding engineering content must carry so that content reads correctly on its own. The
framework supplies none of it.

## Repository entry (planning:repository-entry)

A repo with engineering content carries a README, the `work/` tree of `planning:layout` in [layout.md](./layout.md), and
nothing that needs this framework to be read: no `AGENTS.md`, `CLAUDE.md`, `context/`, or `winter-ext.toml`, no rule
text, no `planning:` id, no tool or extension name. The README opens with a `#` title naming the product's requirements,
such as `# Toolshed requirements`, and directly under it, before any `##`, one paragraph naming the system the
requirements are for and saying the repo holds requirements content only. Its `##` sections follow, one for each `###`
below, starting at Contents. This rule shapes only engineering's part of the intro and of each section; another tier's
part is that tier's, and a section for a tier the repo does not hold is omitted.

<!-- shared:product-intent-cases -->

Product intent lives in one of four places, and each section below that depends on it says how: in this repo; in another
repo; only in a tracker or wiki; or mixed, partly in this repo and partly elsewhere.

<!-- /shared:product-intent-cases -->

Engineering conforms fully in every case; only the Upstream schemes table changes.

### Contents

- In the `Path | What it holds` table, engineering's rows: the root `engineering.md` when present, and, written as
  `work/<initiative>/<epic>/…`, `engineering.md`, `assumptions.md`, `spec.md` or `spec/`, and `slices/`.
- A shared file such as `decisions.md` gets one row, which either tier may write.

### Upstream schemes

- The `Scheme | Resolves to | Example` table `planning:scheme-declaration` in [derivation.md](./derivation.md) owns,
  introduced as how a reader resolves the upstream ids requirements and assumptions cite.
- Its `product:` row by case: in this repo, this repository and where an epic's product requirements are looked up; in
  another repo, that repo's URL and where they are looked up; only in a tracker or wiki, "not used", plus one row per
  tracker or wiki scheme requirements cite; mixed, both kinds of row, each requirement citing whichever scheme the
  README gives for that intent.

### Frontmatter

- A slice's keys — `name`, `external` in its scalar form, `depends-on` with what it may name, and `code`
  (`planning:slice-files` in [slices.md](./slices.md)) — in one short YAML example.
- Unless another tier's part covers them, the keys and values of each `epic.md` engineering keeps for an epic planned in
  a tracker (`planning:tracker-epic`): `epic`, `refinement` and its grades, `status` and its values, and `external` in
  its scalar form.

### Markers

One line per status word engineering content puts in a body: the **Proposed.** marker on a requirement unless another
tier's part covers it, and the **Open.** marker and **Decider:** line on a decision unless another tier's part covers
them.

### Ids

- In the `Prefix | Names | Defined in` table, one row each for `engineering:` and `assume:`, and for `decision:` unless
  another tier's part has it, its Defined in cell naming the file in each work folder and at the root that holds them,
  or the other repo's URL and path.
- How a scoped id carries its owner's epic id, that a bare `engineering:` or `assume:` resolves from the citing folder
  outward to the root, that an id is cited as plain text and found by searching for the heading carrying it, and a link
  to `work/`.

**Detect.** A README missing one of these sections, or naming a rule id, an extension, or a tool.
