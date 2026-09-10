---
name: sdf-orchestration
description: Service skill — loaded by sdf-plan, sdf-research, sdf-implement, and sdf-review; not invoked by the user. Subagent roles (explorer, implementer, validator, reviewer), self-contained dispatch prompts, the validate/review cycle, rework limits, and what the orchestrator never does itself.
---

# orchestration

The orchestrator runs the process and talks to the human; its own session stays clean — process and communication only. Every hands-on artifact, a one-line fix included, is a subagent dispatch. It writes no production code, validates nothing, reviews nothing. Templates and checklists: [protocol.md](references/protocol.md).

## Roles

| Role | Does | Never |
|---|---|---|
| Explorer | read-only investigation of one assigned area; reports findings with file:line evidence | edits, makes decisions |
| Implementer | writes exactly one task, runs the project's checks, fixes its own failures before reporting | declares done without checks, expands scope |
| Validator | checks one dispatch: diff scope, conventions, typecheck, runnable scenarios | edits code |
| Reviewer | audits a milestone diff against the plan: traceability, reuse, minimalism | edits code |

The author never validates or reviews their own work; no agent holds two roles.

## Dispatch prompts

A subagent sees neither the plan nor the orchestrator's context. Every prompt carries: scope (the task verbatim, with R# / UC# / DEC# trace), context (stack facts, patterns, fixtures), conventions (from AGENTS.md), skills to load first (from the plan's skill table), the four binding principles, the execution protocol (any doubt → come back with a question, never guess), bans (no commits, no files outside the task), and the report format. Template: [protocol.md](references/protocol.md).

## Cycle

    mini-plan → implementer → validator → reviewer
      → [rework → validator → reviewer]* → accept → update plan → next

Mini-plan before every milestone: files, dispatch order, validation commands, exit criteria. Parallelize by default — tasks with disjoint file sets and closed dependencies dispatch together, each implementer with its own validator. Rework is a new dispatch with a concrete defect list ("try better" is not one); limit 2 rounds per defect, then stop and offer the human 1–2 options. Scenarios that cannot run yet go on the deferred list with their unlocking milestone — they surface at the final gate, never dropped silently.
