---
name: implement
description: Execute a task plan milestone by milestone through subagents — an implementer writes, a validator checks, a reviewer audits; progress, deviations, and blockers are written back to plan.md so any new session can resume from the repository. Use after plan has produced a READY plan.
---

# implement

Role: orchestrator, and your session stays clean — process and communication only. Everything hands-on goes through subagent dispatches (the `orchestration` skill), however small: code, checks, research, fixes. You write no production code, validate nothing, review nothing, commit nothing — shipping is ship's job. Parallelize dispatches as far as the plan's dependency graph allows.

## 0. Load state

**Input.** The optional argument names the plan: a path to plan.md, a task slug under docs/plans/active/, or free text matched against plan titles. No argument and exactly one READY or IN_PROGRESS plan → take it. Several candidates → list them and ask. None → stop and ask.

Spec first: read AGENTS.md, then that plan's spec.md: requirements, use cases, and scenarios are the goal side. Only then plan.md, the how. Status must be READY, IN_PROGRESS, or BLOCKED; anything else → stop and ask. BLOCKED is loadable only to re-present its blocking questions and unblock — no dispatches until one is resolved. Read every ADR the plan links.

Branch main → stop: propose a task branch `<type>/<slug>`; proceed only on consent. A dirty worktree is the normal mid-task state for an IN_PROGRESS plan: verify the uncommitted changes trace to the plan's milestones and DEV records; anything that traces to nothing → stop and ask (commit via ship, stash, or remove — the human picks).

## 1. Session resume

Trust the plan, verify the code — full protocol in [references/session-resume.md](references/session-resume.md). A milestone marked [x] must match reality; a mismatch gets corrected and reported. Then take the first unchecked milestone.

## 2. Milestone loop

Per [references/milestone-cycle.md](references/milestone-cycle.md):

    mini-plan → dispatch implementer → validator → milestone reviewer
      → [rework → validator → reviewer]* → accept

Goal first: a milestone opens by restating the R# / UC# and the spec scenario it serves, and that scenario is the milestone's exit criterion. Code no use case needs is out of scope, however useful it looks. Four principles govern you and every subagent you raise: think before coding, simplicity first, surgical changes, goal-driven execution. They outrank convenience.

One plan task per dispatch; every role (implementer, validator, reviewer) is a freshly raised subagent, and the orchestrator never edits, validates, or reviews by itself. Re-check the plan's skill table for this milestone against the environment (the `skill-matrix` skill) and load the matches before dispatching.

Validation is continuous: the implementer runs the project's checks and fixes its own failures before reporting, an independent validator checks every dispatch, the reviewer audits every milestone close. Neither step is ever skipped, and the loop repeats until the verdicts are clean. Rework limit: 2 rounds per defect, then stop with options for the human.

## 3. Write back

After each milestone: tick it, refresh Progress (Current / Next / Blocked) in plan.md, record deviations (DEV) and new questions (Q). A Level 3 discovery mid-build → RFC → human → ADR (the `decisions` skill), plan updated — no silent architecture changes.

A blocking question marks its milestone [!] and its Q BLOCKED, and stops that thread; independent milestones keep moving, so the plan status stays IN_PROGRESS. The plan itself goes BLOCKED only when nothing can proceed. Unblocking: the human's answer, in this session or a fresh one, is recorded verbatim in the Q record (RESOLVED + Resolution), the milestone marker flips back, and a BLOCKED plan returns to IN_PROGRESS. An L3 unblock goes RFC → decision → ADR first.

## 4. Final gate

- no pending or in-progress todos; every milestone [x];
- the deferred-scenario list is empty — everything ran;
- full Validation section executed: commands + manual scenarios, dispatched to a validator with the complete checklist;
- every deviation discovered during the run has a DEV record in the plan — none left only in the chat;
- report: milestones, touched files, validation results, open assumptions;
- status → IN_REVIEW, hand to review. APPROVE → the human ships, and `ship` closes the plan (DONE, Result, move to docs/plans/completed/). NEEDS CHANGES → review returns the status to IN_PROGRESS and the loop resumes.

## Execution protocol

Any doubt → stop and ask. Guessing is prohibited — for you and for every subagent you dispatch.
