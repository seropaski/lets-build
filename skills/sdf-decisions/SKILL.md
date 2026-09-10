---
name: sdf-decisions
description: Service skill — loaded by sdf-plan, sdf-research, sdf-implement, and sdf-review; not invoked by the user. Decision levels, the question ladder (the human resolves every question), the RFC and ADR lifecycle, and epoch-based document naming.
---

# decisions

ONLY THE HUMAN RESOLVES A QUESTION — information the request, the code, or a linked document does not state explicitly is asked about, never assumed. This skill supplies the machinery. Full rules: [decision-rules.md](references/decision-rules.md). Formats: [templates.md](references/templates.md).

## Levels

- **L1 — what the code dictates.** Variable names, function splitting, equivalent forms. Execution, not a decision. The label never hides a question: two options implying different behavior for the user are L2.
- **L2 — task-scoped.** "Reuse the existing DataTable". Put to the human with alternatives; stored as a DEC record tracing to the answer.
- **L3 — architectural.** Binds future work: a shared abstraction, a new data flow, a heavyweight dependency. Route: RFC → human decision → ADR → plan links the ADR.

Test: would a future engineer ask "why is it built this way?" → L2 at least; L3 if the answer constrains other features.

## Question ladder

1. Does the existing code answer it? Read and move on.
2. Does the request, spec, contract, or an ADR answer it? Take it from there.
3. Ask the human — the only remaining step. Q record in plan.md; BLOCKED if milestones wait on it. Reversibility changes the cost of a wrong guess, not the right to guess.

## RFC — a question put to the human

Drafted the moment an L3 fork appears: problem, options, trade-offs, a recommendation with a stance. Decided → write the ADR; the RFC takes its final status and links it. Deferred → Q record; dependent milestones blocked. Rejected with a direction → the direction constrains the plan; if itself L3, it gets the ADR.

## ADR — a decision already made

Written at acceptance — never speculatively, never after the code silently committed everyone. Context, decision, alternatives, consequences, Origin link to the RFC. A mid-build L3 discovery (sdf-implement) runs the same loop: RFC → human → ADR → plan updated with a DEV record.

## Naming

Globally numbered documents and task dirs take an epoch-milliseconds id — counters collide across machines, epochs do not:

    docs/architecture/rfc/1786584699364-entity-reference-registry.md
    docs/architecture/adr/1786584701127-server-state-management.md
    docs/plans/active/1786584705221-orders-status-filter/

Task-local counters (UC, DEC, DEV, Q) stay per-file. Generation commands and collision handling: [decision-rules.md](references/decision-rules.md).
