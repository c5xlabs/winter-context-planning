# Specs

The technical contracts in a work folder's `spec.md`: how the folder's requirements are to be built.

## Spec contracts (planning:spec-contracts)

When an epic's implementation mechanics serve readers different from its requirements, give it a `spec.md`, or once it
grows, a `spec/` of leaves (`planning:file-or-folder`). A spec is written for a senior engineer who thinks in contracts,
interfaces, domain models, and payloads, so it is artifact-first and prose is usually unnecessary. `spec.md` holds these
`##` sections, in this order, each optional:

1. `System` — components and services and what talks to what: a diagram, a component list, a service table, or code;
   external services the epic depends on, with the limits and timeouts the design relies on.
2. `Domain` — types and interfaces in the system's language; a state diagram where state matters.
3. `Interfaces` — endpoints with method, path, and request, response, and error payloads with status codes; events by
   name and payload type; internal abstractions by signature.
4. `Flows` — sequence diagrams for behaviour that crosses services, failure and retry paths included, external services'
   among them.
5. `Data` — schema as DDL or tables, plus migrations.
6. `Open questions` (`planning:inline-questions` in [decisions.md](./decisions.md)).

A `spec/` leaf is named freely — by use case, contract, or area, whichever reads best — and uses any of these sections,
or others it needs; there is no index. In either form code blocks and diagrams come first, and a sentence states only
what no artifact can, such as idempotency, ordering, or failure behaviour, preferably as a comment inside the artifact,
in the engineering voice (`planning:engineering-voice` in [voice.md](./voice.md)). An `engineering:` or `product:` id is
mentioned where a piece serves it, often in a code comment, and resolves outward like any bare id; no line lists what
the spec satisfies, and no requirement is restated.

Prose belongs to the requirement. The engineering requirement states the behaviour and its reason; the spec cites it by
id and shows only the contract or flow that delivers it. A requirement, then the spec fragment answering it:

```markdown
## Reserve once (engineering:reserve-once)

A retried reservation request never creates a second reservation for the same pickup window, whether the client or a
worker retries it.

Acceptance:

- Replaying a reservation request returns the first reservation and creates no second one.
```

```ts
// engineering:reserve-once
// POST /tools/{toolId}/reservations, Idempotency-Key: <uuid>
async function reserve(toolId: string, windowId: string, key: string): Promise<Reservation> {
  const claimed = await requests.insertPending({ key, toolId, windowId }); // unique on key: a replay loses the insert
  if (!claimed) {
    const prior = await requests.findByKey(key);
    return prior.status === "pending" ? retryLater() : prior.reservation; // 409 while the winner is still reserving
  }
  const reservation = await reservations.create(toolId, windowId); // only the winner creates the reservation
  await requests.complete(key, reservation);
  return reservation;
}
```

Never: narrative paragraphs; rationale or options weighed, which is a decision's; landing order or task steps;
verification sections; metrics, alerts, or logging targets, which are requirements; UX definition, which stays with the
upstream intent; a routing index; a `What already holds` or carry-over section. A decision that overtakes a spec
corrects it in place, or deletes a leaf that no longer applies.

## Shared contracts (planning:shared-contracts)

A contract several specs answer to has one home: a leaf of the spec of the epic that owns the capability it describes
(`planning:capability-epics`). Every other spec links the parts it builds and never copies them; there is no
`contracts/` folder.

## Spec freeze (planning:spec-freeze)

A spec freezes when its epic is delivered and moves with it to `delivered/` (`planning:delivered-archive` in
[layout.md](./layout.md)); what is built is documented in the owning project repo, not here. Later work on the same
capability is a new epic with a spec of its own, which cites the frozen one where it builds on it and never edits or
deletes it.
