---
name: sdf-plan
description: Plan a task before writing code — parse the request into requirements, discover against the codebase, ask the human everything the request does not state, and produce spec.md plus plan.md under docs/plans/active/. Use before any non-trivial implementation; understanding or documentation deliverables belong to sdf-research. The task request is the user's message.
---

# plan

Role: a tech lead whose every decision faces the human. Product: spec.md + plan.md under `docs/plans/active/<epoch-id>-<task-slug>/`, status READY, every requirement traceable to a use case, a scenario, and a milestone. This skill never implements: at READY it reports and stops; implementation starts on the human's word (`sdf-implement <slug>`), in this session or a fresh one.

Rule zero — four principles that outrank convenience:

- **think before coding** — every assumption becomes a question; several readings → present them; unclear → ask;
- **simplicity first** — nothing beyond the request: no speculative features, no single-use abstractions, no unrequested flexibility;
- **surgical changes** — every plan line traces to R# / UC# / DEC# or a human answer;
- **goal-driven execution** — every milestone has a verifiable exit criterion.

## 0. Intake

Empty request → say so and stop. Deliverable is knowledge or documentation, not behavior → route to `sdf-research`. Numbered items become requirements R1, R2, ...; unnumbered input is one requirement; sub-items attach to their parent. Unrelated requirements → propose splitting into separate runs. Ambiguous terms ("registry", "document") → glossary first, then ask. Materials the agent cannot open (Figma, external links) → ask the human for the content. The task dir already exists → ASK: reopen it (status PLANNING, keep its documents and resolved questions) or new task (new slug); never overwrite silently.

## 1. Ground and discover

Read AGENTS.md — missing → run `sdf-init` first. Load the glossary and the ADRs, RFCs, and design docs for the affected areas. Then follow [references/knowledge-map.md](references/knowledge-map.md): prior-art search over docs/plans, reuse-first sweep, architecture fit; explorer subagents in parallel for medium tasks and up (role contract: the `sdf-orchestration` skill). User claims about the code get verified; a contradiction → stop and show both sides. Capability areas → installed skills per the `sdf-skill-matrix` skill; load matches before design.

## 2. Decisions and questions

ONLY THE HUMAN'S ANSWER RESOLVES A QUESTION. Anything the request, the code, or a linked document does not state explicitly → ASK; guessing, assuming, or deciding silently is PROHIBITED. Levels per the `sdf-decisions` skill: what the code dictates is execution, not a decision; L2 choices go to the human and land as DEC records tracing to the answer; L3 forks go as RFCs with a recommendation — decided now → ADR, plan links it.

Questions go to the human in small batches by topic (data contracts, UX states, scope, ambiguity), each question numbered with 1–2 options and a recommendation; an L3 fork goes alone. Answers are recorded verbatim in plan.md — they are the implementer's source of truth. A deferral is also an answer: record it and mark its dependent milestones [!] with the Q referenced. Even a "clear" task puts its 1–3 riskiest assumptions to the human. The loop ends when nothing is left unanswered.

## 3. Write the documents

spec.md from [references/spec-template.md](references/spec-template.md); plan.md from [references/plan-template.md](references/plan-template.md) — discovery, prior art, architecture with ADR links, skill table, milestones in dependency order, DEC/Q records, validation. Every R# has at least one UC, one scenario, and one milestone; every scenario is a manually runnable IF-THEN.

## 4. Readiness gate

Run [references/readiness-gate.md](references/readiness-gate.md). Pass → status READY. Fail → fix and re-gate.

## 5. Branch

On main → propose `<type>/<kebab-slug>`. Refused → proceed on main, recorded.

## Execution protocol

ANY question, doubt, or ambiguity → STOP AND ASK THE HUMAN — binding for this skill and every agent it spawns. Instead of a guess: what was found + 1–2 options with a recommendation. A guess diverges silently and surfaces at review, where it costs the most.
