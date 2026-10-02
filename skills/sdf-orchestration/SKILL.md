---
name: sdf-orchestration
description: Service skill, loaded by lets-plan, lets-research, lets-implement, and lets-review; not invoked by the user. Subagent roles (explorer, implementer, validator, reviewer), self-contained dispatch prompts, how subagents ask questions, the validate and review cycle, rework limits, and what the orchestrator never does itself.
---

# sdf-orchestration

The orchestrator runs the process and talks to the human. Subagents write, check, and review the code, each in a fresh context, so the orchestrator's session stays small and nobody grades their own work. The orchestrator writes only process records: plan.md, spec.md, and the documents its calling skill gives it. The glossary and the conventions it writes only after the human approves the exact text, per `sdf-doc-standards`; subagents only propose changes to them. Every code change is a dispatch, a one-line fix included. Templates and checklists: [references/protocol.md](references/protocol.md).

## Roles

| Role | Does | Never |
|---|---|---|
| Explorer | read-only investigation of one assigned area; reports findings with file:line evidence | edits, makes decisions |
| Implementer | writes exactly one task, runs the project's checks, fixes its own failures before reporting | declares done without checks, widens the scope |
| Validator | checks one dispatch: diff scope, conventions, typecheck, runnable scenarios | edits code |
| Reviewer | audits a milestone diff against the plan: traceability, reuse, minimalism | edits code |

The author of a change never validates or reviews it, and no agent holds two roles.

## Questions

Subagents don't talk to the human. When a subagent hits something that the task, the code, and the docs don't answer, it stops and returns the question with what it found, one or two options, and a recommendation. The orchestrator puts it to the human per the `sdf-decisions` question ladder and dispatches again with the answer.

## Dispatch prompts

A subagent sees neither the plan nor the orchestrator's context, so the prompt has to carry everything it needs. The template in [references/protocol.md](references/protocol.md) lists what that is; leave nothing out, the trust rule included.

## Cycle

    mini-plan → implementer → validator → reviewer
      → [rework → validator → reviewer]* → accept → update plan → next

Before every milestone, write a mini-plan: files, dispatch order, validation commands, exit criteria. Parallelize by default: tasks with disjoint file sets and finished dependencies go out together, each implementer with its own validator. Parallel tasks share one worktree, so give each validator its own task's file list and those of the other running tasks. A typecheck error in another task's files is reported but not counted against this one.

Rework is a new dispatch with a concrete defect list; "try harder" is not a defect list. Each defect gets two rounds at most. After that, stop and give the human one or two options with a recommendation. A scenario that can't run yet goes on the Deferred scenarios list in plan.md with the milestone that unlocks it, so it comes back at the final gate instead of getting lost.

## Without subagents

If the run needs subagents and the agent can't spawn them, tell the human before starting. One agent playing every role loses the independent check this workflow is built on. Go ahead that way only on the human's explicit yes, and note it in plan.md Progress.
