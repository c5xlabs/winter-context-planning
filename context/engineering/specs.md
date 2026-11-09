# Specs

A work folder's `spec.md` holds the technical contracts: how the folder's requirements get built.

## Spec contracts (planning:spec-contracts)

Give an epic a `spec.md` when its implementation mechanics serve different readers from its requirements, and split it
into a `spec/` folder of leaves once it grows (`planning:file-or-folder`). The reader is a senior engineer who thinks in
contracts, interfaces, domain models, and payloads, so a spec is mostly artifacts.

`spec.md` uses these `##` sections, in this order, each optional:

1. `System` — what talks to what, as a diagram, component list, service table, or code; the external services the epic
   depends on, with the limits and timeouts the design relies on.
2. `Domain` — types and interfaces in the system's language, plus a state diagram where state matters.
3. `Interfaces` — endpoints with method, path, and request, response, and error payloads with status codes; events by
   name and payload type; internal abstractions by signature.
4. `Flows` — sequence diagrams for behaviour that crosses services, including failure and retry paths.
5. `Data` — schema as DDL or tables, plus migrations.
6. `Open questions` (`planning:inline-questions`).

A `spec/` leaf is named by whatever reads best — use case, contract, or area — uses any of these sections or others it
needs, and has no index.

In either form, artifacts come first. A sentence says only what no artifact can, such as idempotency, ordering, or
failure behaviour, ideally as a comment inside the artifact and in the engineering voice (`planning:engineering-voice`).
Mention an `engineering:` or `product:` id where a piece serves it, often in a code comment, but never list what the
spec satisfies or restate a requirement. The requirement carries the prose, the behaviour and its reason; the spec shows
only the contract or flow that delivers it. A requirement, then the spec fragment answering it:

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

Some things look at home in a spec but belong elsewhere: rationale and options weighed go in a decision; metrics,
alerts, and logging targets are requirements; and UX definition stays with the upstream intent. A spec also has no
narrative paragraphs, landing order or task steps, verification sections, routing index, or `What already holds` or
carry-over section.

When a decision overtakes a spec, correct the spec in place, or delete a leaf that no longer applies.

## Shared contracts (planning:shared-contracts)

A contract several specs answer to lives in one place: a leaf of the spec of the epic that owns the capability it
describes (`planning:capability-epics`). Other specs link the parts they build rather than copying them, and there is no
`contracts/` folder.

## Spec freeze (planning:spec-freeze)

A spec freezes when its epic is delivered and moves with it to `delivered/` (`planning:delivered-archive`). What got
built is documented in the owning project repo, not here. Later work on the same capability is a new epic with its own
spec, which cites the frozen one where it builds on it and never edits or deletes it.
