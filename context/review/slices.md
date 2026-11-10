# Slice review rubric

A cut is ready to build when its slices collectively deliver the epic through changes that can each land and be
verified. Assessment and finding weight use `planning:review-assessment`, `planning:review-finding-weight`, and
`planning:review-stage`.

## Slice dimensions (planning:slice-review)

Coverage belongs to the whole cut; acceptance and landing are also judged per slice. Merely naming a requirement is not
delivery evidence, and counting slices or changed lines is not a size assessment. A different valid cut is not a defect.

### Complete cut

Every requirement, acceptance bullet, and spec section can be traced to a slice that delivers it, including failure
behavior and any required migration or closing step.

### Derivation

Each slice's behavior and acceptance are grounded in its cited sources. The slice does not introduce a design fact that
belongs in a requirement, assumption, decision, or spec.

### Dependency correctness

Every prerequisite provides a mechanism the slice actually needs. Every needed artifact can be produced before use,
without cycles or hidden ordering.

### Independent landing

The slice can merge with its checks passing without requiring unlanded work, exposing unfinished behavior, or breaking
the applicable compatibility promise.

### Verifiability

Acceptance checks exercise the changed behavior through existing methods or methods built by the work. The evidence
distinguishes success from the relevant failure.

### Cohesion and size

The change is one reviewable mechanism or entrypoint, not unrelated work bundled together or a cut so small that it
cannot land on its own.

### Delivery strategy

The sequence implements the applicable migration or rollout strategy through its closing step. A feature flag is not
assumed to be temporary merely because it is a flag.

### Boundaries

Ownership of shared changes is clear, with deferred work explicit and neither gaps nor duplicate implementations between
slices.

## Artifact fit (planning:slice-review-fit)

`planning:slice-files` governs each file; `planning:slice-cuts` and `planning:slice-order` govern the cut and its
dependencies. `planning:slice-lifecycle` governs identity when re-slicing. The assessment checks those contracts without
requiring speculative code pointers or a particular task tracker.

Verification and guidance may be introduced by the foundation being planned rather than assumed to exist already. Their
placement is judged by whether each change can be built, reviewed, and verified as it lands, not by a fixed
documentation-first or documentation-last order. A missing source contract is a spec or requirement gap, not design work
to hide inside a slice.
