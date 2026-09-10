---
name: sdf-implement
description: Execute a READY plan milestone by milestone through subagents — an implementer writes, a validator checks, a reviewer audits; progress, deviations, and blockers are written back to plan.md so any session resumes from the repository. Use after sdf-plan reports READY.
---

# implement

Role: orchestrator — process and communication only; every hands-on step is a subagent dispatch (the `sdf-orchestration` skill). You write no code, validate nothing, review nothing, commit nothing (that is `sdf-ship`). Parallelize as far as the plan's dependency graph allows.

## 0. Load state

The optional argument names the plan: path to plan.md, task slug under docs/plans/active/ (epoch prefix optional), or free text matched against titles. No argument and exactly one READY or IN_PROGRESS plan → take it; several → list and ask; none → stop and ask.

Read AGENTS.md, then the plan's spec.md (the goal side), then plan.md (the how). Status must be READY, IN_PROGRESS, or BLOCKED — anything else → stop and ask; BLOCKED loads only to re-present its questions, no dispatches until one resolves. Read every ADR the plan links. On main → stop, propose `<type>/<slug>`, proceed on consent. A dirty worktree is normal mid-task: verify the uncommitted changes trace to milestones/DEV; untraceable → stop and ask.

## 1. Resume

Trust the plan, verify the code — [references/session-resume.md](references/session-resume.md). A milestone [x] must match reality; a mismatch is corrected and reported. Take the first unchecked milestone.

## 2. Milestone loop

Per [references/milestone-cycle.md](references/milestone-cycle.md). A milestone opens by restating its R# / UC# and spec scenario — that scenario is the exit criterion; code no use case needs is out of scope. One plan task per dispatch; every role a fresh subagent. Re-check the skill table against the environment (`sdf-skill-matrix`) before dispatching. Validation is continuous and never skipped; rework limit 2.

## 3. Write back

After each milestone: tick, refresh Progress, record DEV and new Q. A question the plan does not answer → Q record and the human's answer — the implementer decides nothing beyond what the plan states. An L3 discovery → RFC → human → ADR, plan updated; no silent architecture. A design doc's area changed behavior → the doc is updated within the same milestone. A blocking question marks its milestone [!] and stops that thread; independent milestones continue; the plan goes BLOCKED only when nothing can move. An unblock — the human's answer, in any session — is recorded verbatim and the thread resumes.

## 4. Final gate

- every milestone [x], no pending todos, the deferred-scenario list empty;
- the full Validation section executed: commands + manual scenarios, dispatched to a validator;
- every deviation has a DEV record; the design docs of touched areas are still true;
- report: milestones, files, validation results, questions resolved (Q records);
- status → IN_REVIEW, hand to `sdf-review`. APPROVE → the human ships; `sdf-ship` closes the plan. NEEDS CHANGES → review returns the status to IN_PROGRESS.

## Execution protocol

ANY question, doubt, or ambiguity → STOP AND ASK THE HUMAN — for you and every subagent you dispatch. A question costs a minute; a guessed change surfaces at review.
