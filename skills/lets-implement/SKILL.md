---
name: lets-implement
description: Execute a READY plan milestone by milestone through subagents, where an implementer writes, a validator checks, and a reviewer audits. Progress, deviations, and blockers go back into plan.md, so any session can resume from the repository. Use after lets-plan reports READY, or to resume a plan in progress.
---

# lets-implement

You are the orchestrator: you run the process and talk to the human. Writing, validating, and reviewing code are subagent dispatches per the `lets-orchestration` skill. You write only plan.md, plus an RFC or ADR when the human settles an L3 question. Committing belongs to `lets-ship`. Parallelize as far as the plan's dependency graph allows.

## 0. Load state

The optional argument names the plan: a path to plan.md, a task slug under `<docs-root>/plans/active/` (with or without the epoch prefix), or free text matched against plan titles. With no argument, take the plan if exactly one is READY, IN_PROGRESS, or BLOCKED. If there are several, list them and ask; if there are none, stop and ask.

Read AGENTS.md, then spec.md (the goal), then plan.md (the how), then every ADR the plan links. Load `lets-doc-standards` and `lets-decisions`. The status decides what happens next:

- READY: implementation hasn't started. Set IN_PROGRESS and begin at M1.
- IN_PROGRESS: resume, step 1.
- BLOCKED: present the blocking questions again and dispatch nothing until one is answered.
- PLANNING, IN_REVIEW, or DONE: not this skill's job. Say which skill owns it and stop.

Compare the current branch with the plan's Branch field. If the plan's branch is checked out in another worktree (`git worktree list`), that worktree is where the plan lives: point the human at its path and stop. On the default branch with no recorded choice, stop and propose `<type>/<slug>`; offer to create it in a worktree of its own ([references/worktree.md](references/worktree.md)) instead of switching this checkout — the natural choice when another task is in flight here. Continue once the human decides. Uncommitted changes are normal mid-task, but each one must trace to a milestone or a DEV record. If something doesn't, stop and ask.

## 1. Resume

Trust the plan, but check it against the code: [references/session-resume.md](references/session-resume.md). A ticked milestone must match the worktree; fix a mismatch and report it. Then take the first unchecked milestone that isn't blocked.

## 2. Milestone loop

Follow [references/milestone-cycle.md](references/milestone-cycle.md). Open each milestone by restating its R#, UC#, and spec scenario. That scenario is the exit criterion, and code no use case needs is out of scope. One plan task per dispatch, and a fresh subagent for every role. Check the plan's skill table against the installed skills (`lets-skill-matrix`) before dispatching. Validation runs after every dispatch and is never skipped.

## 3. Write back

After each milestone, tick it, refresh Progress, and record DEVs and new Qs. When the plan doesn't answer something, the implementer brings the question back and you ask the human; nobody decides anything the plan doesn't state. An L3 discovery goes through an RFC, the human, and an ADR, and then the plan is updated. Architecture never changes silently.

Subagents report proposed glossary and convention changes, for example a new entity or a renamed one. Put each to the human with the exact text, write it only after they approve it (`lets-doc-standards`), and record the answer as a Q. Until it's answered, the milestone stays open.

A blocking question marks its milestone [!] and stops that thread only; independent milestones carry on. The plan becomes BLOCKED only when nothing can move. When the human answers, in this session or a later one, record the answer word for word, set the Q to RESOLVED, and resume the thread.

## 4. Final gate

- Every milestone is [x], or the human dropped it from scope and a DEV record says so.
- The Deferred scenarios list is empty.
- A validator ran the whole Validation section: the commands and the manual scenarios.
- Every deviation has a DEV record, and the design docs of the touched areas are still true.
- Every glossary and convention proposal has the human's answer, and the glossary matches the domain terms in the code.

Then report the milestones, the files, the validation results, and the questions resolved. Set the status to IN_REVIEW and stop. The next step is `lets-review`, on the human's word.
