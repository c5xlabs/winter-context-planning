# Derivation

How each engineering requirement ties back to the product intent it serves, wherever that intent lives: this repo,
another repo, a tracker, or a wiki.

## Serving product intent (planning:serves)

Every requirement says in its prose which product intent it serves, through at least one upstream id: "Serves
`product:card-hold`." Schemes can be mixed freely. Cite the most specific intent that exists, so a product requirement
rather than its epic, and a story rather than its tracker epic.

A standalone constraint (`planning:engineering-constraints`) is the one requirement without an upstream id, since nobody
upstream asked for it. A feature requirement whose product intent isn't written yet is not a constraint: record an
assumption (`planning:assumption-record`) and serve that.

## Upstream schemes (planning:upstream-schemes)

Upstream ids take the form `<scheme>:<key>`, and only these schemes are allowed:

| Scheme         | Form                                        | Names                                               |
| -------------- | ------------------------------------------- | --------------------------------------------------- |
| `product:`     | `product:<owner id>/<subject>`, or bare     | One product requirement                             |
| `epic:`        | `epic:<epic id>`                            | A whole epic, when no requirement of it fits        |
| `assume:`      | `assume:<owner id>/<subject>`, or bare      | An assumption record in a folder's `assumptions.md` |
| tracker / wiki | `<scheme>:<native key>`, as `jira:SHED-123` | An item, keyed as that system keys it               |

The framework fixes `product:`, `epic:`, and `assume:`. Tracker and wiki schemes are the repo's to declare, and so is
where `product:` resolves; don't guess, read the scheme table.

A `product:` id's owner is the id of whatever holds the requirement: `<epic>` or `<initiative>/<epic>`, an initiative or
project slug, or nothing for the program. It is never a path, so the id survives an epic's move to `delivered/` but
changes when the epic moves into or out of an initiative. The subject is the `## <Name> (product:<subject>)` heading in
the epic's `requirements.md`, or the `###` heading under `## Requirements` in its `epic.md` when the records are inline.
An owner never uses the slug of an initiative or epic beneath it as a subject, so a full id always reads unambiguously.
A bare subject resolves outward from the citing folder through its initiative and project to the program
(`planning:bare-ids`).

Cite a whole epic as `epic:<epic id>`, never as a `product:` id without a subject. Keeping product ids stable is the
product tier's job.

A tracker id is written exactly as the `external:` value that names the same item in an `epic.md`
(`planning:tracker-epic`). When the tracker key changes, update both in place.

Milestones, personas, jobs, and raw URLs are not upstream ids.

## Scheme declaration (planning:scheme-declaration)

The repo's README carries an `Upstream schemes` table with the columns `Scheme | Resolves to | Example`. It has a
`product:` row always, plus one row for each other scheme any requirement or assumption cites, added in the same change
as that scheme's first citation. Every row has an example.

- `product:` resolves to the repo and file holding an epic's product requirements, or "not used". `epic:` resolves to
  the same place and gets no row of its own.
- `assume:` resolves to the `assumptions.md` of the folder whose requirements rest on it; for a bare id, the nearest one
  outward.
- A tracker or wiki scheme resolves to its base URL plus the project key or space.

```markdown
| Scheme     | Resolves to                                                 | Example                                      |
| ---------- | ----------------------------------------------------------- | -------------------------------------------- |
| `product:` | not used                                                    | —                                            |
| `assume:`  | `assumptions.md` in the folder citing it                    | `assume:volunteer-shifts/cover-max-duration` |
| `jira:`    | `https://tracker.toolshed.example/browse/` — project `SHED` | `jira:SHED-412`                              |
```
