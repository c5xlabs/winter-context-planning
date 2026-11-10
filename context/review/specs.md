# Spec review rubric

A spec is ready to build from when it supplies a feasible, consistent technical design for its requirements without
leaving consequential choices to the builder. Assessment and finding weight use `planning:review-assessment`,
`planning:review-finding-weight`, and `planning:review-stage`.

## Spec dimensions (planning:spec-review)

The applicable cases depend on the system; the rubric does not require retries, persistence, services, or security
mechanisms where the work has none. Routine implementation choices can remain local. Missing choices matter when they
change a contract, ownership boundary, compatibility promise, or the way correctness is established.

### Requirement coverage

Each product acceptance criterion and engineering commitment has an identifiable contract or flow. The design does not
silently narrow a requirement or invent one.

### Contract completeness

Interfaces, types, state transitions, and ownership are precise enough that independent implementations would agree on
observable behavior.

### Failure behavior

The design defines relevant invalid input, partial failure, timeout, cancellation, retry, and cleanup cases, not only
the successful path.

### Technical feasibility

The selected mechanisms and dependencies support the promised behavior within the stated platform, version, and system
limits.

### Architectural fit

The design honors applicable target boundaries and shared contracts. Intended changes are explicit, with no hidden
cross-component ownership.

### Internal consistency

Types, examples, interfaces, flows, and configuration agree, including contracts shared across spec leaves or epics.

### Decision readiness

The builder can proceed without choosing unstated product behavior or settling an open architectural decision the design
depends on.

### Scope and complexity

The design solves the bounded capability without requiring speculative abstractions or adjacent capabilities.

## Artifact fit (planning:spec-review-fit)

`planning:spec-contracts` governs the spec's shape; `planning:shared-contracts` governs a contract answered by several
specs. The assessment is whether the design is unambiguous and its authoritative contracts can be found, not whether a
reviewer prefers different section names or more prose.

Intent that the design needs but product has not stated is judged against `planning:assumption-record`; derivation uses
`planning:serves`. A spec cannot settle missing product intent merely by specifying an implementation. Rationale,
requirements, and landing order retain their own homes.
