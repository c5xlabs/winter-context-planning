# Decisions

Product and engineering record decisions (`decision:`) in one shared format.

## The decision bar (planning:decision-bar)

A decision is a real choice between alternatives, the kind someone could later ask "why this and not that?" about. An
answer that only clarifies what was meant is not a decision; it edits the requirement or spec.

"Can the calendar service publish the roster as a feed?" has a true answer that nobody chose. "Do we let a shift
volunteer extend a loan without the coordinator's say?" is a commitment, so it needs a decision. In the same way,
choosing time-boxed roles over per-user grants for coordinator cover is a decision, but finding that the identity
provider caps role lifetimes at 90 days is a fact.

## Decision ids (planning:decision-slugs)

A decision's id names the subject decided, not the edit that recorded it: `decision:<owner id>/<subject>`, or
`decision:<subject>` for a program-wide decision. It always carries its owner and is never cited bare; owner ids and the
project-relative form follow `planning:owned-scoped-ids` and `planning:bare-ids`. Product and engineering share the
namespace, so two decisions in one owner's file never share a subject. The id stays the same when an open decision is
made and when a made one is overturned.

## The decisions file (planning:decisions-file)

A folder's `decisions.md` holds both product's and engineering's decisions in a single list: a `#` title naming the
folder, then the open decisions, then the made ones, newest first. There are no per-tier decision files. The file is
created along with the folder's first decision.

Keep it plain: no dates, no tables, no Context, Decision, or Consequences subsections, and no monthly or other
per-period files.

## Decision format (planning:decision-format)

Each decision is a `##` section with the id in parentheses after its name. An optional `**Decider:**` line names who
decides, a person or a group (`product` and `engineering` are groups like any other). The body is one or two sentences
saying what was decided and why. There are no other fields and no decision indexes; git history records when.

A decision is either open or made. A call that is deliberately deferred is an open decision. Its body starts with
**Open.** and says what must be decided and which ids it blocks:

```markdown
## Volunteers per shift (decision:volunteer-shifts/volunteers-per-shift)

**Decider:** coordinator

**Open.** Whether a shift puts one volunteer on the counter by default or two sharing it, so pickups keep moving while
one checks a return; it blocks `product:shift-roster`.
```

Making the decision rewrites the same entry without the marker and moves it to the top of the made decisions:

```markdown
## Volunteers per shift (decision:volunteer-shifts/volunteers-per-shift)

**Decider:** coordinator

Each shift puts one volunteer on the counter by default, because shifts that shared the counter between two volunteers
left members waiting for each to assume the other had them.
```

Overturning a made decision also rewrites the same entry, saying what is decided now and why.

## Decision ownership (planning:decision-ownership)

A decision belongs to the epic, initiative, or project whose delivery it constrains most. A decision that is local to
one epic stays with that epic. An initiative owns the decisions about its direct scope and those spanning several of its
epics, and a project owns those cutting across its epics. Calls that cut across projects, or across epics in a repo
without projects, belong to the program and live in the root `decisions.md`.

The decision lives only in its owner's `decisions.md`. Any document it binds cites its id rather than copying it. When a
decision overtakes other documents, they change as `planning:change-in-place` describes. A decision that no longer
applies, open or made, is deleted, and the same change corrects everything that cited it.

## Inline questions (planning:inline-questions)

A clarifying question, one whose answer will say what was meant rather than choose between alternatives, sits in the
file it concerns. Any requirements or spec file may end with an `## Open questions` section of plain bullets without
ids, each naming who can answer it. For engineering content that means `engineering.md` or the spec, or in folder form
the leaf the question concerns. When a question is answered, fold the answer into the text and delete the bullet. There
is no separate questions file and no other tracking.

If a question can't be answered without choosing, make it an open decision instead.
