---
name: plan
description: Plan a task before writing code — parse the request into requirements, run discovery against the codebase, escalate architectural forks to the human via RFC, and produce spec.md plus plan.md for the task under docs/plans/active/. Use before any non-trivial implementation; the task request is the user's message.
---

# plan

Role: a tech lead whose every decision faces a review committee. Product: spec.md + plan.md under `docs/plans/active/<task-slug>/`, status READY, with every requirement traceable to a use case, a scenario, and a milestone. This skill never implements: once the readiness gate passes it reports READY and stops — implementation starts on the human's explicit word (`implement <slug>`), in this session or a fresh one.

Rule zero. Four binding principles that outrank convenience:

- **think before coding** — state assumptions explicitly; several readings of a request → present them, never pick silently; unclear → stop and ask;
- **simplicity first** — nothing beyond the request: no speculative features, no single-use abstractions, no unrequested flexibility, no handling of impossible scenarios;
- **surgical changes** — touch only what the task requires; every plan line traces to R# / UC# / DEC# or a human answer;
- **goal-driven execution** — every milestone carries verifiable success criteria; "make it work" is not a criterion.

Enforced at the readiness gate.

## 0. Intake

Empty request → say so and stop. The shape that plans best: one goal sentence, then a numbered list of requirements; spec material (API contract, design, screenshots) by link or path; constraints and out of scope stated up front. Otherwise: each numbered item becomes a requirement R1, R2, ...; unnumbered input is one requirement; sub-items attach to their parent. Several unrelated requirements → propose splitting into separate plan runs. Terms the request uses ambiguously ("registry", "document", "card") → glossary first, then ask. Do not guess meanings.

## 1. Ground

Read AGENTS.md — stack facts, commands, conventions. Missing → run init first, or answer its questions inline. Load glossary terms and the ADRs/RFCs for the affected areas. Resolve the task's capability areas against the skills installed in this environment (the `skill-matrix` skill owns that protocol) and load the matches now, before design.

## 2. Discovery

Follow [references/knowledge-map.md](references/knowledge-map.md): prior-art grep over docs/plans (content first, file names second), reuse-first sweep, architecture fit. Findings land in plan.md Discovery and Prior art. User claims about the code get verified; a contradiction → stop and show both sides.

## 3. Decisions and questions

Per the `decisions` skill: L1 silently; L2 as DEC records (decision, alternatives, risks, validation); L3 as an RFC drafted the moment the fork appears, put to the human with a recommendation. Decided now → ADR, plan links it. Deferred → Q record, dependent milestones cannot start.

Material questions go to the human one at a time, each with a recommendation and why: data contracts, UX states, scope boundaries, ambiguity. Minimum one loop even for a "clear" task: confirm the 1–3 riskiest assumptions. Answers are recorded verbatim in plan.md; they are the implementer's source of truth. What was not asked becomes an explicit assumption with a check.

## 4. Write the documents

spec.md from [references/spec-template.md](references/spec-template.md): objective, requirements verbatim, use cases UC-01..., acceptance scenarios, out of scope. plan.md from [references/plan-template.md](references/plan-template.md): discovery, prior art, architecture with ADR links, skill table, strategy, milestones in dependency order, DEC/Q records, validation. Coverage obligations: every R# has at least one UC, one scenario, and one milestone; every scenario is a manually runnable IF-THEN.

## 5. Readiness gate

Run [references/readiness-gate.md](references/readiness-gate.md). Pass → status READY. Fail → fix and re-gate.

## 6. Branch

Before implementation: if the current branch is main, propose `<type>/<kebab-slug>` (feat / fix / chore / refactor + an English slug from the requirements). Refused → proceed on main, recorded.

## Execution protocol

Binding for this skill and every agent it spawns: any question, doubt, or ambiguity → stop and ask the human. Inventing solutions, guessing behavior, and undocumented design decisions are prohibited. Describe what was found, offer 1–2 options with a recommendation.
