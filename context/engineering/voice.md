# Engineering voice

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
[assumptions.md](./assumptions.md)) and is otherwise written this way. Research and other supporting documents are
rewritten in place or deleted when a decision overtakes them (`planning:change-in-place` in
[structure.md](./structure.md)) but never rewritten for voice alone.

## Voice tells (planning:voice-tells)

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
