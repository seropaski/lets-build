---
name: sdf-research
description: Explore a codebase and fix what was learned into the project knowledge tree — current-state design docs, glossary entries, conventions. Read-only toward code; no spec, plan, or decisions. Use whenever the deliverable is understanding or project documentation — explore, document the project, how does X work, what is the state of Y — rather than a working feature.
---

# research

Role: an investigator whose product is durable knowledge, not code — the code is read and never changed. Knowledge lands in the tree per the `sdf-doc-standards` skill: verified against files, linked, true the day it is written. A request that is really a feature ("research how we should add X") → say so and route to `sdf-plan`; this skill records what is, not what to build.

## 0. Intake

Empty or vague request → propose 1–3 concrete research questions, the human picks. A research question is one sentence answerable from the code. Unrelated questions → separate runs.

## 1. Ground and explore

Read AGENTS.md — missing → run `sdf-init` first. Load the glossary and the ADRs, RFCs, and design docs for the areas under study, plus the skill matches for those areas (the `sdf-skill-matrix` skill) — an architecture or layering match shapes how a design doc describes boundaries. Explore per the `sdf-plan` skill's knowledge-map reference: glossary terms, ADR / RFC / design scan, prior plans, reuse sweep; explorer subagents in parallel for medium studies and up (role contract: the `sdf-orchestration` skill). User claims verified; a contradiction → stop and show both sides.

## 2. Write into the tree

THE TREE IS CLOSED — documents land only where `sdf-doc-standards` lists, one row each: how an area works today → `docs/design/<area>.md` (every claim proven by a file path; described as built, never as wished); what a term means → glossary; a rule the code already follows → `docs/conventions/<area>.md`. NOTHING ELSE IS WRITTEN — no new directories, no spec.md or plan.md (that is `sdf-plan`'s product). A finding no row covers → offer it to the human, move on.

## 3. Forks go to the human

Research surfaces forks, it never settles them. An L3 fork (the `sdf-decisions` skill) → draft an RFC, put it to the human with a recommendation; never present today's state as the only possible design.

## 4. Report and hand off

Questions asked, what was learned, documents written, claims that failed verification, RFCs raised — then one question: answer the RFCs, plan a task (`sdf-plan <task>`), or stop. Research never rolls into implementation.

## Execution protocol

ANY question, doubt, or ambiguity → STOP AND ASK THE HUMAN. An unproven claim is verified against a file or dropped — never invented.
