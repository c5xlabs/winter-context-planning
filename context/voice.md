# Voice

Product content and engineering content each have their own voice. Each voice applies to its own tier's files. Research,
decision records, and other supporting documents stay out of scope. They are rewritten in place or deleted when a
decision overtakes them (`planning:change-in-place`), but never rewritten just for voice.

## Product voice (planning:product-voice)

The charter, the registries, `epic.md`, `initiative.md`, and `requirements.md` are product intent. Write them as an
experienced product owner who knows the domain and can make one idea useful to a customer, a product leader, and an
engineer:

- **Begin with the person and the problem.** Say whose work is hard and what that costs before naming the response.
- **Use connected prose.** Lists are for facts that really are parallel. They are not a substitute for showing how one
  idea leads to the next.
- **State the concept before the mechanism.** The person's need comes before models, APIs, components, or events.
- **Use precise language without ornament.** No sales adjectives, slogans, or layered hedging. A technical term earns
  its place by carrying exact meaning, and it is explained where the audience may not share it.
- **Bridge disciplines with a concrete moment.** When a concept risks going abstract, show a person at the point where
  it matters.

> A shift volunteer should not phone three members to find out who still wants a ladder that just came back. When a
> reservation lapses, the shed offers the ladder to the first member waiting for it, who confirms it themselves, and the
> volunteer steps in only when a request needs a judgment call.

## Product voice tells (planning:product-voice-tells)

These tells sound fluent and say little. Rewrite them when you find them:

- **Bullet cascades** carrying an argument that needed connected sentences.
- **Sales adjectives**, such as *seamless*, *robust*, *powerful*, and *intuitive*, which praise the product instead of
  describing it.
- **Triads** chosen for rhythm: "fast, simple, and reliable".
- **"Not just X but Y"**, which invents a lesser claim to beat.
- **An opener that restates the heading** before saying anything new.
- **Layered hedging**, as in "could potentially help to enable", where the owner should say what they mean.
- **Jargon without a bridge**: a term used in place of an explanation for a reader who does not share it.

> **Avoid:** Reservation management is a key capability. The system will provide robust, configurable reservation
> workflows, intelligent reminders, and real-time notifications, empowering members to not just reserve tools but
> maximize shelf utilization.

> **Hit:** A member who reserved a tool and never came should not keep it off the shelf for a week. A missed pickup
> waits on the pickup shelf until the shift closes, then goes back into the catalog, and the member is told their
> reservation lapsed.

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
