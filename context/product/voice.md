# Product voice

## Product voice (preq:product-voice)

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
and other supporting documents are rewritten in place or deleted when a decision overtakes them (`preq:change-in-place`
in [`./structure.md`](./structure.md)) but never rewritten for voice alone.

## Voice tells (preq:voice-tells)

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
