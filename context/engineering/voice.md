# Engineering voice

Research, decision records, and other supporting documents are out of scope: they are rewritten in place or deleted when
a decision overtakes them (`planning:change-in-place`), but never rewritten just for voice.

## Engineering voice (planning:engineering-voice)

`engineering.md`, `assumptions.md`, `spec.md` or `spec/`, `slices/`, and engineering's entries in `decisions.md` are
engineering content. Write them as a senior software engineer writing for other engineers who will build to it, test it,
and get paged for it. An assumption is the one exception: it still states its intent in product terms
(`planning:assumption-record`).

- **Statements, not stories.** Say what the system does, under what conditions, and how you would test it. Lead with the
  requirement, then give its reason or cite the product requirement it serves. Scenes and personas belong to product.
- **Common terms, in their basic form.** Write retry, timeout, idempotent, queue, cache, rate limit, transaction,
  schema, endpoint, event, p95 latency. Prefer "retry" to "redelivery semantics" and "background job" to "saga
  orchestration". Use a niche term only when you need its exact meaning.
- **Precise and testable.** Give numbers with units, bounds, and time windows. Say what happens on failure, on timeout,
  and at the limit.
- **What an engineer needs.** Cover interfaces, data, invariants, failure modes, limits, and operability. Cite the
  product backstory instead of retelling it.
- **Short declarative sentences.** Lists are fine for parallel constraints. Engineering content does not need the
  connected prose that product intent does.

> A reservation still unclaimed when its shift closes is released within 60 s of the close. A release returns the tool
> to the catalog and emits one `reservation.lapsed` event. Serves `product:no-show-release`.

## Engineering voice tells (planning:engineering-voice-tells)

These tells sound fluent and say little. Rewrite them when you find them:

- **Filler verbs**, such as *ensure*, *leverage*, *facilitate*, and *enable*, where the sentence should say what the
  system does.
- **Sales adjectives**, such as *robust*, *seamless*, *scalable*, and *comprehensive*, which promise instead of specify.
- **Triads** chosen for rhythm: "reliable, performant, and secure".
- **Layered hedging**, as in "should typically aim to", where a requirement should state a bound.
- **An opener that restates the heading** before saying anything new.
- **Meta lines**: "This section describes…", "Note that…".
- **Em-dash chains** stacking asides into one sentence.
- **Bold-label bullet cascades** standing in for plain constraints.
- **A narrated user story** where a statement would do.

> **Avoid:** To ensure a seamless reservation experience, the system will leverage a robust, scalable notification
> pipeline. When a reservation is confirmed — whether in the app or at the counter — volunteers should typically be
> notified in a timely manner.

> **Hit:** The pickup list receives each `reservation.confirmed` event within 10 s at p95. A failed delivery is retried
> with backoff for 15 min, then raises an alert.
