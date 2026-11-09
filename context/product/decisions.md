# Decisions

Decisions (`decision:`), product's and engineering's alike: what earns one, how one is identified, where it lives, how
an open one is held until it is made, and where a clarifying question goes instead.

## The decision bar (preq:decision-bar)

<!-- shared:decision-bar -->

A decision is a genuine choice between real alternatives, one someone could later reasonably ask "why this and not
that?" about. An answer that only clarifies what was meant edits the requirement and never becomes a record.

<!-- /shared:decision-bar -->

"Can the calendar service publish the roster as a feed?" has a true answer nobody chose, so it edits the requirement;
"Do we let a shift volunteer extend a loan without the coordinator's say?" is a commitment and needs a decision.

## Decision ids (preq:decision-slugs)

<!-- shared:decision-slugs -->

Every decision, product's or engineering's, carries a stable `decision:` id naming the subject decided, not the edit
that recorded it, scoped to its owner — `decision:<owner id>/<subject>`, always written in full, or `decision:<subject>`
when it is program-wide. Both tiers share the namespace, so no two decisions in one owner's file share a subject. The id
stays when an open decision is made and when a made one is overturned.

<!-- /shared:decision-slugs -->

Scoping follows `preq:owned-scoped-ids` in [`./namespaces.md`](./namespaces.md).

## The decisions file (preq:decisions-file)

<!-- shared:decisions-file -->

A folder's `decisions.md` holds both tiers' decisions in one list, in order:

1. A `#` title naming the folder.
2. The open decisions.
3. The made decisions, newest first.

Never: dates; Context, Decision, or Consequences subsections; monthly or other per-period files; tables. The root
`decisions.md` holds the program's, for calls that cut across epics. Both tiers' decisions share the one list and the
`decision:` namespace, so there are no per-tier decision files. The file is created with the folder's first decision.

<!-- /shared:decisions-file -->

## Decision format (preq:decision-format)

<!-- shared:decision-format -->

Each decision is a `##` section of its owner's `decisions.md`: a heading naming the decision with its id in parentheses;
optionally, one line right under it naming who decides, a person or a group, `product` and `engineering` being groups
like any other — `**Decider:** engineering`, `**Decider:** Dana Reyes`; then one or two sentences stating what was
decided and why. A decision is open or made, and has no other status. A call deliberately deferred is an open decision:
its body starts **Open.** and says in one or two sentences what must be decided and what it blocks, cited by id. Making
it rewrites the same entry as a made decision, dropping the marker and keeping its id, and moves it to the top of the
made ones. Overturning a made decision rewrites the same entry under the same id to state what is decided now and why.
There are no other fields and no decision indexes: the owner's file is the list, and history carries when.

<!-- /shared:decision-format -->

```markdown
## Volunteers per shift (decision:volunteer-shifts/volunteers-per-shift)

**Decider:** coordinator

**Open.** Whether a shift puts one volunteer on the counter by default or two sharing it, so pickups keep moving while
one checks a return; it blocks `product:shift-roster`.
```

Made, the same entry reads:

```markdown
## Volunteers per shift (decision:volunteer-shifts/volunteers-per-shift)

**Decider:** coordinator

Each shift puts one volunteer on the counter by default, because shifts that shared the counter between two volunteers
left members waiting for each to assume the other had them.
```

## Decision ownership (preq:decision-ownership)

<!-- shared:decision-ownership -->

A decision belongs to the epic or initiative whose delivery it constrains most, or to the program when no single one's
does. Its one home is the owner's folder's `decisions.md`, or the root's for the program, and a scoped id's scope is
that owner's id. A document elsewhere that it binds cites its id and never copies it. A decision that no longer applies
at all, open or made, is deleted, and whatever cited it is corrected in the same change.

<!-- /shared:decision-ownership -->

An initiative owns decisions about its direct scope or spanning several of its epics; a decision local to one epic stays
with that epic.

## Inline questions (preq:inline-questions)

<!-- shared:inline-questions -->

A clarifying question — one whose answer will say what was meant, not choose between alternatives — sits in the file it
concerns. Any requirements or spec file may end with an `## Open questions` section of plain bullets, with no ids, each
naming who can answer it. When one is answered, fold the answer into the text and delete the bullet; history keeps the
question. A question nobody can answer without choosing is an open decision instead. Clarifying questions are tracked
nowhere else, and there is no separate questions file.

<!-- /shared:inline-questions -->
