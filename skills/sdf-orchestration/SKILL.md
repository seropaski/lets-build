---
name: sdf-orchestration
description: Service skill — loaded by the sdf-implement and sdf-review skills; not invoked by the user. The subagent protocol (three separated roles, self-contained dispatch prompts, the validate and review cycle, rework limits, and what the orchestrator must never do itself).
---

# orchestration

The orchestrator runs the process and talks to the human. Its own session stays clean: process and communication only — every hands-on artifact, however small (a one-line fix included), is a subagent dispatch. It writes no production code, validates nothing, reviews nothing; every artifact comes from a subagent whose role differs from the author's. Prompt templates and checklists: [protocol.md](references/protocol.md).

## Roles

| Role | Does | Never |
|---|---|---|
| Implementer | writes code for exactly one task, then runs the project's checks and fixes its own failures before reporting | declares done without running the checks, expands scope |
| Validator | checks one dispatch: diff scope, conventions, typecheck, runnable scenarios | edits code |
| Reviewer | audits a finished milestone's diff against the plan: traceability, reuse, minimalism | edits code |

The author never validates or reviews their own work, and no agent holds two roles.

## Self-contained dispatch prompts

A subagent sees neither the plan nor the orchestrator's context. Every prompt carries:

- scope — the task from the plan, verbatim (what changes, where, why);
- context — stack facts, touched modules, patterns to follow, contracts and fixtures;
- conventions — from AGENTS.md: layers, import alias, slice public APIs;
- skills — the ones the plan's skill table assigns to this task, loaded before code;
- behavior — four binding principles: think before coding (assumptions explicit, unclear → stop and ask), simplicity first (nothing beyond the task), surgical changes (task files only, no "improvements" of adjacent code), goal-driven execution (say how you will verify before you code);
- the execution protocol — any doubt: come back with a question, do not guess;
- bans — no commits, no files outside the task;
- report format — files changed, what was done, how checked, open questions.

## Cycle

    mini-plan → dispatch implementer → validator → milestone reviewer
      → [rework → validator → reviewer]* → accept → update plan → next

- a mini-plan precedes every milestone: files, dispatch order, validation commands, exit criteria;
- parallelize by default: dispatch together every group of tasks with disjoint file sets and closed dependencies, checked against the plan before dispatching; serialize only tasks that genuinely overlap, and give each parallel implementer its own validator (the validators also run in parallel);
- rework means a new dispatch with a concrete defect list — "try better" is not a defect list;
- rework limit: 2 rounds per defect, then stop: show the human what was tried, offer 1–2 options with a recommendation;
- scenarios that cannot run yet go on the deferred list with the milestone that unlocks them; they surface at the final gate, never dropped silently.
