---
name: decisions
description: Service skill — loaded by the plan, implement, and review skills; not invoked by the user. Decision levels (silent / plan-recorded / human-owned), the question ladder, the RFC and ADR lifecycle, and epoch-based naming for globally numbered documents.
---

# decisions

Architectural decisions are the one part of the workflow a human owns. This skill keeps that boundary and supplies the machinery: levels, the question ladder, RFC, ADR, naming. Full rules: [decision-rules.md](references/decision-rules.md). Formats: [templates.md](references/templates.md).

## Levels

- **L1 — implementation detail.** Variable names, how to split a function, which of two equivalent JSX forms. Decide silently, document nothing.
- **L2 — task-scoped.** "Reuse the existing DataTable", "no new state library". DEC record in plan.md: decision, alternatives, risks, validation.
- **L3 — architectural.** Binds future work: a shared abstraction other features must adopt, a new data flow, a heavyweight dependency. Route: RFC → human decision → ADR → plan links the ADR. Never skip the human.

Test: would a future engineer ask "why is it built this way?" That is L2 at least, L3 if the answer constrains other features.

## Question ladder

Walk down, stop at the first step that answers:

1. Does the existing code answer it? Read and move on.
2. Does the spec, API contract, design, or an ADR answer it? Take it from there.
3. Cheaply reversible? Decide, record as L2.
4. Ask the human. Q record in plan.md; BLOCKED if milestones wait on it.

Guessing at step 4 breaks the workflow's one hard rule.

## RFC — a question put to the human

Draft the RFC the moment a Level 3 fork appears during planning: problem, options, trade-offs, a recommendation with a stance. Statuses: Proposed → Accepted / Rejected / Superseded / Deferred. Outcomes:

- decided now → write the ADR, RFC takes its final status and links the ADR, the plan references the ADR;
- deferred → RFC stays Proposed or Deferred, Q record goes into the plan, dependent milestones cannot start;
- rejected with a direction → the direction constrains the plan; if that direction is itself L3, it gets the ADR.

## ADR — a decision already made

Written at the moment of acceptance — never speculatively, never after the code has silently committed everyone. Content: context, decision, alternatives, consequences, Accepted + date, Origin link to the RFC. The RFC links back. During implement, a new L3 discovery runs the same loop: RFC → human → ADR → plan updated with a DEV record.

## Naming

Globally numbered documents (RFC, ADR) take an epoch-milliseconds id. Different people plan on different machines; a shared counter would collide, epoch ids do not:

    docs/architecture/rfc/1786584699364-entity-reference-registry.md
    docs/architecture/adr/1786584701127-server-state-management.md

Task-local counters (UC, DEC, DEV, Q) stay per-file — they live inside one plan and never cross machines. Generation commands and collision handling: [decision-rules.md](references/decision-rules.md).
