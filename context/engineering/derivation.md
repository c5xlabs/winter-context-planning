# Derivation

Tying each engineering requirement to the product intent it serves, wherever that intent lives — this repo, another
repo, a tracker, or a wiki.

## Serving product intent (planning:serves)

Every requirement names the product intent it serves in its prose — "Serves `product:card-hold`." — through at least one
upstream id, `<scheme>:<key>` in any mix of schemes (`planning:upstream-schemes`), citing the most specific intent that
exists: a product requirement over its epic, and a story over its tracker epic. The one exception is a standalone
constraint (`planning:engineering-constraints` in [engineering.md](./engineering.md)), which nobody upstream asked for
and stands without one. A feature requirement whose product intent is not written yet is not a constraint: record an
assumption (`planning:assumption-record`) and serve it.

## Upstream schemes (planning:upstream-schemes)

Cite upstream intent only through these schemes:

| Scheme              | Form                                                                                                   | Names                                                                                                                                   |
| ------------------- | ------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------- |
| `product:`          | `product:<epic id>/<subject>` or `product:<initiative>/<subject>`, or a bare subject, resolved outward | One of an epic's product requirements, or a requirement binding every epic of an initiative, where the README's scheme table points     |
| `epic:`             | `epic:<epic id>`                                                                                       | A whole epic, when no requirement of it is specific enough to cite, at its `epic.md` — in this repo, or where the `product:` row points |
| `assume:`           | `assume:<owner id>/<subject>`, or a bare `assume:<subject>`, resolved outward                          | An assumption record in a folder's `assumptions.md` (`planning:assumption-record`)                                                      |
| Tracker/wiki scheme | `<scheme>:<native key>` — `jira:SHED-123`, `linear:ENG-42`, `confluence:<page id>`                     | An item in a tracker or wiki, keyed as that system keys it; the repo names the scheme in its scheme table                               |

The framework fixes `product:`, `epic:`, and `assume:`; tracker and wiki schemes are the repo's to declare. Never guess
where `product:` resolves — read the scheme table. A `product:` id names one product requirement. Its scope is the
epic's id — `<epic>` or `<initiative>/<epic>` — never a path, so it survives delivery's move to `delivered/` but changes
when the epic moves into or out of an initiative; its final `/<subject>` is the `## <Name> (product:<subject>)` heading
in the epic's `requirements.md`, or the `###` one under `## Requirements` in its `epic.md` when the records are inline.
A whole epic is cited as `epic:<epic id>`, never as a `product:` id without a subject. An initiative's own `product:`
subject is never one of its epics' slugs, so the segments of a full id read unambiguously; a bare subject resolves
outward from the citing folder, no further than the initiative, since the root holds no `product:` (`planning:bare-ids`
in [namespaces.md](./namespaces.md)). Milestones, personas, and jobs are not upstream ids, and product ids' stability is
the product tier's to keep. A tracker id is written exactly as the `external:` value naming the same item in an
`epic.md` (`planning:tracker-epic` in [layout.md](./layout.md)); when its key moves, update both in place. A raw URL is
not an upstream id.

## Scheme declaration (planning:scheme-declaration)

The repo, not the framework, says where each scheme resolves. Its README carries an `Upstream schemes` table —
`Scheme | Resolves to | Example` — with one row per scheme any requirement or assumption cites, added in the same change
as the scheme's first citation:

- `product:` — where an epic's product requirements are looked up: the repo and the file holding them, or "not used".
  `epic:` resolves where this row points and takes no row of its own.
- `assume:` — the `assumptions.md` of the folder whose requirements rest on it; a bare id, the nearest one outward.
- each tracker or wiki scheme — the base URL plus the project key or space.

Every row has an example; there is always a `product:` row.

```markdown
| Scheme     | Resolves to                                                 | Example                                      |
| ---------- | ----------------------------------------------------------- | -------------------------------------------- |
| `product:` | not used                                                    | —                                            |
| `assume:`  | `assumptions.md` in the folder citing it                    | `assume:volunteer-shifts/cover-max-duration` |
| `jira:`    | `https://tracker.toolshed.example/browse/` — project `SHED` | `jira:SHED-412`                              |
```
