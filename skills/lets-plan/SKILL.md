---
name: lets-plan
description: Plan a task before writing code. Turns the request into numbered requirements, checks them against the codebase, asks the human everything the request leaves open, and writes spec.md and plan.md under the docs root recorded in AGENTS.md. Use before any non-trivial change. When the deliverable is understanding or documentation rather than behavior, use lets-research instead.
---

# lets-plan

You act as a tech lead who takes every decision to the human. The product is spec.md and plan.md in `<docs-root>/plans/active/<epoch-id>-<task-slug>/` (the docs root AGENTS.md records), status READY, with every requirement traced to a use case, a scenario, and a milestone. This skill never implements. At READY it reports and stops; implementation starts when the human runs `lets-implement <slug>`, in this session or a fresh one.

Four principles outrank convenience:

- **Think before coding.** Every assumption becomes a question. If the request can be read several ways, present the readings.
- **Simplicity first.** Nothing beyond the request: no speculative features, no single-use abstractions, no flexibility nobody asked for.
- **Surgical changes.** Every plan line traces to an R#, UC#, DEC#, or a human answer.
- **Goal-driven.** Every milestone has an exit criterion someone can check.

## 0. Intake

The task is the user's message. If it's empty, say so and stop. If the deliverable is knowledge or documentation rather than behavior, hand it to `lets-research`.

Numbered items become requirements R1, R2, and so on; sub-items stay under their parent; unnumbered input is a single requirement. If the requirements are unrelated, propose splitting them into separate runs. Look up ambiguous terms ("registry", "document") in the glossary first, then ask. If the request points at material you can't open (Figma, external links), ask the human for its content.

If the task dir already exists, ask whether to reopen it (status back to PLANNING, its documents and resolved questions kept) or to start a new task under a new slug. Never overwrite it silently.

## 1. Ground and discover

Read AGENTS.md. If it's missing, stop and suggest `/lets-init`. Load the `lets-doc-standards` skill and run its discovery protocol (references/discovery.md): the glossary, the ADRs and design docs for the affected areas, prior plans, the reuse sweep, and explorer subagents for medium tasks and up. Verify every claim the user makes about the code; if the code disagrees, stop and show both sides. Then match the capability areas to installed skills per `lets-skill-matrix`, and load the matches before designing.

## 2. Questions and decisions

Load `lets-decisions` and climb its question ladder for every open point. What the code dictates is execution. L2 choices go to the human and become DEC records that cite the answer. L3 forks become RFCs with a recommendation, and a decided RFC becomes an ADR that the plan links.

Ask the way the ladder describes, batching by topic: data contracts, UX states, scope, ambiguity. The answers go into plan.md word for word, because the implementer treats them as the source of truth. Even a task that looks clear puts its one to three riskiest assumptions to the human. If the human defers a question, record it as BLOCKED with "deferred by the human" and mark its milestones [!]. Keep asking until no question is OPEN.

Two kinds of answers also change shared docs, and both need the human's approval of the exact text (`lets-doc-standards`):

- a term the task introduces, renames, or gives a new meaning: propose its glossary entry;
- a DEC that sets a rule for code from now on: propose the convention.

Put each proposal to the human as its own numbered question, write what they approve during planning, and record the outcome as a Q. A rejected proposal stays out of the glossary and conventions, and the spec doesn't rely on it.

## 3. Write the documents

spec.md from [references/spec-template.md](references/spec-template.md), plan.md from [references/plan-template.md](references/plan-template.md). Every R# gets at least one UC, one scenario, and one milestone, and every scenario is an IF-THEN a person can run by hand.

## 4. Branch

If you're on the default branch, propose `<type>/<kebab-slug>` and create it when the human agrees. Write the result into plan.md's Branch field. If the human prefers to stay on the default branch, write that down too, so later skills don't ask again.

## 5. Readiness gate

Run [references/readiness-gate.md](references/readiness-gate.md). If anything fails, fix it and run the gate again. When everything passes, set the status to READY, report with the next command (`lets-implement <slug>`), and stop.
