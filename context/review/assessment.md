# Review assessment

The shared assessment concepts for planning-artifact rubrics. Execution, report format, and remediation belong to the
person or automation using the rubric.

## Assessment dimensions (planning:review-assessment)

An assessment distinguishes the following judgments for each applicable dimension. These are scoring concepts, not a
required output schema. An average score cannot cancel an acceptance-blocking gap; unresolved evidence is neither proof
of failure nor a passing assessment.

### Sound

Evidence supports the criterion at the artifact's intended stage.

### Gap

Evidence shows that a criterion is not met.

### Unresolved

The evidence or decision needed to judge the criterion is missing.

### Not applicable

The criterion does not apply to this work or stage, with a reason.

## Finding weight (planning:review-finding-weight)

A finding identifies the affected passage or omission, its governing criterion, the consequence, and the correction
needed. A preferred alternative is not a defect unless the chosen approach fails a criterion. An unresolved question
blocks only the readiness claim that depends on its answer.

### Acceptance-blocking

A binding promise or constraint is violated, or a missing contract, decision, or verification basis prevents the work
from being built or judged correct at the intended stage.

### Improvement

The artifact supports correct, verifiable work, but could be clearer, smaller, or easier to use.

## Stage and evidence (planning:review-stage)

Readiness is relative to the artifact being judged, not to a fully implemented product. Missing downstream artifacts are
not defects before their stage: a spec need not already have slices, and a greenfield repository need not already have
the architecture guidance or verification tools the work explicitly establishes.

Planned bootstrap work must still make each dependent change's correctness assessable as it lands. A planned test is
evidence that a contract can be verified, not evidence that its implementation already passes. Existing code or tool
behavior can substantiate feasibility or expose a contradiction without turning an artifact review into implementation.

The rubric does not add product promises or application policies. Applicable requirements, constraints, decisions, and
target-owned conventions supply those criteria; an omitted policy that affects readiness is an unresolved choice, not
permission for a reviewer to invent one.
