# Requirements review rubric

Requirements are sound when they express bounded, testable promises and engineering commitments that serve the stated
intent. Assessment and finding weight use `planning:review-assessment`, `planning:review-finding-weight`, and
`planning:review-stage`.

## Requirement dimensions (planning:requirements-review)

### Intent and clarity

The requirements identify what changes and for whom, with enough precision to judge whether the promise holds. A builder
does not have to choose unstated product behavior to interpret them.

### Testable acceptance

Product acceptance describes observable outcomes. Engineering acceptance can be checked by a test or measurement;
subjective qualities are not treated as measurable bounds.

### Product and engineering separation

Engineering commits to what is needed beyond the product text rather than restating it. Implementation mechanics do not
masquerade as requirements, and standalone engineering constraints do not need an invented product parent.

### Derivation

Each feature-oriented engineering commitment serves the most specific live intent available. The cited source exists and
still says what the commitment relies on; its location follows the repository's declared upstream schemes.

### Coverage and bounds

Engineering commitments address the product promises that need them and respect applicable parent constraints. A derived
bound still keeps the product promise; a technical convenience does not silently narrow it.

### Assumptions and decisions

Intent that engineering needs but product has not stated is explicit as an assumption, not quietly chosen in a
requirement or spec. Confirmed or refused assumptions do not remain open. Missing clarification or decisions are
visible, with their effect on readiness clear.

### Consistency and relevance

The requirements agree with one another and the current intent. Engineering records that serve no live intent and are
not standalone constraints do not remain binding; citations do not point to removed or contradicted records.

### Downstream alignment

Where specs and slices exist, their contracts and delivery coverage still support the requirements and acceptance
criteria they derive from. Their absence before the relevant stage is not a coverage failure.

## Artifact fit (planning:requirements-review-fit)

Classification uses `planning:classify-requirement`; product and engineering records use `planning:requirement-records`
and `planning:requirement-record`. Derivation and constraints use `planning:serves`, `planning:beyond-product`, and
`planning:engineering-constraints`. Assumptions and open questions retain the homes defined by
`planning:assumption-record` and `planning:inline-questions`.

The review judges current alignment without rewriting frozen delivered work (`planning:delivered-archive`). A
requirement's meaning, a spec's design, and a slice's cut are separate concerns; a correction belongs at the source of
the gap rather than being hidden in a downstream artifact.
