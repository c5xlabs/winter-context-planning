# Voice

Product content and engineering content are written in different voices, each binding its own tier's files.

## Product voice (planning:product-voice)

Write product intent — the charter, registry entries, epic and initiative intent, requirement records, and capability
descriptions — as an experienced product owner who knows the domain and can make one idea useful to a customer, a
product leader, and an engineer:

- **Begin with the person and the problem.** Say whose work is hard and what that costs before naming the response.
- **Use connected prose.** Lists are for genuinely parallel facts, not a substitute for explaining how one idea leads to
  the next.
- **State the concept before the mechanism.** The person's need comes before models, APIs, components, or events.
- **Use precise language without ornament.** No sales adjectives, slogans, or layered hedging; a technical term earns
  its place by carrying exact meaning, and is explained where the audience may not share it.
- **Bridge disciplines with a concrete moment.** When a concept risks going abstract, show a person at the point where
  it matters.

> A shift volunteer should not phone three members to find out who still wants a ladder that just came back. When a
> reservation lapses, the shed offers the ladder to the first member waiting for it, who confirms it themselves, and the
> volunteer steps in only when a request needs a judgment call.

This binds the charter, the registries, `epic.md`, `initiative.md`, and `requirements.md`. Research, decision records,
and other supporting documents are rewritten in place or deleted when a decision overtakes them
(`planning:change-in-place` in [`./structure.md`](./structure.md)) but never rewritten for voice alone.

## Product voice tells (planning:product-voice-tells)

Drafts drift into a register that sounds fluent and says little. Catch these tells and rewrite them:

- **Bullet cascades** carrying an argument that needed connected sentences.
- **Sales adjectives** — *seamless*, *robust*, *powerful*, *intuitive* — which praise the product instead of describing
  it.
- **Triads** reached for by rhythm: "fast, simple, and reliable".
- **"Not just X but Y"**, which invents a lesser claim to beat.
- **An opener that restates the heading** before saying anything new.
- **Layered hedging** — "could potentially help to enable" — where the owner should say what they mean.
- **Jargon without a bridge**: a term doing the work of an explanation for a reader who does not share it.

The same requirement, badly and then well:

> **Avoid:** Reservation management is a key capability. The system will provide robust, configurable reservation
> workflows, intelligent reminders, and real-time notifications, empowering members to not just reserve tools but
> maximize shelf utilization.

> **Hit:** A member who reserved a tool and never came should not keep it off the shelf for a week. A missed pickup
> waits on the pickup shelf until the shift closes, then goes back into the catalog, and the member is told their
> reservation lapsed.

## Engineering voice (planning:engineering-voice)

Write engineering content as a senior software engineer writing for other engineers: someone who will build to it, test
it, and get paged for it.

- **Statements, not stories.** Say what the system does, under what conditions, and how you would test it. Lead with the
  requirement, then give its reason or cite the product requirement it serves. Scenes and personas are product's job.
- **Common terms, in their basic form.** Write retry, timeout, idempotent, queue, cache, rate limit, transaction,
  schema, endpoint, event, p95 latency. Prefer "retry" to "redelivery semantics" and "background job" to "saga
  orchestration"; use a niche term only when its exact meaning is needed.
- **Precise and testable.** Give numbers with units, bounds, and time windows. Say what happens on failure, on timeout,
  and at the limit.
- **What an engineer needs.** Cover interfaces, data, invariants, failure modes, limits, and operability. Cite product
  backstory instead of retelling it.
- **Short declarative sentences.** Lists are fine for parallel constraints. Unlike product intent, engineering content
  does not need connected prose.

> A reservation still unclaimed when its shift closes is released within 60 s of the close. A release returns the tool
> to the catalog and emits one `reservation.lapsed` event. Serves `product:no-show-release`.

This binds `engineering.md`, `assumptions.md`, `spec.md` or `spec/`, `slices/`, and engineering's entries in
`decisions.md`; an assumption still states its intent in product terms (`planning:assumption-record` in
[`./assumptions.md`](./assumptions.md)) and is otherwise written this way. Research and other supporting documents are
rewritten in place or deleted when a decision overtakes them (`planning:change-in-place` in
[`./structure.md`](./structure.md)) but never rewritten for voice alone.

## Engineering voice tells (planning:engineering-voice-tells)

Drafts drift into a register that reads fluent and says little. Catch these tells and rewrite them:

- **Filler verbs**: *ensure*, *leverage*, *facilitate*, *enable*, where the sentence should say what the system does.
- **Sales adjectives**: *robust*, *seamless*, *scalable*, *comprehensive*, which promise instead of specify.
- **Triads** reached for by rhythm: "reliable, performant, and secure".
- **Layered hedging**: "should typically aim to", where a requirement states a bound.
- **An opener that restates the heading** before saying anything new.
- **Meta lines**: "This section describes…", "Note that…".
- **Em-dash chains** stacking asides into one sentence.
- **Bold-label bullet cascades** standing in for plain constraints.
- **A narrated user story** where a statement would do.

The same requirement, badly and then well:

> **Avoid:** To ensure a seamless reservation experience, the system will leverage a robust, scalable notification
> pipeline. When a reservation is confirmed — whether in the app or at the counter — volunteers should typically be
> notified in a timely manner.

> **Hit:** The pickup list receives each `reservation.confirmed` event within 10 s at p95. A failed delivery is retried
> with backoff for 15 min, then raises an alert.
