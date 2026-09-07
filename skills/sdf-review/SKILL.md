---
name: sdf-review
description: Two-layer review of a change — compliance with the task's spec, plan, and ADRs, then a high-confidence code review across six tracks (security, performance, business logic, deploy safety, duplication, dead code). Advisory only; no edits until the full review is written and the human asks for fixes. Input optional scope word, commit, branch, or PR; empty input reviews uncommitted changes.
---

# review

Advisory by default: write the complete review first, offer fixes after. Never flag outside the layers and tracks below. Prefer no finding over a weak finding.

## Layer 0 — context

If the change belongs to a plan (docs/plans/active/): read its spec.md, plan.md, and linked ADRs; Layer 1 applies. If not, the change is a drive-by and only Layer 2 applies, and the review says so up front.

## Layer 1 — compliance

[references/compliance.md](references/compliance.md): does the diff implement every requirement, follow the plan's strategy, respect the ADRs, and hold to the four binding principles (think before coding, simplicity first, surgical changes, goal-driven execution)? An undocumented deviation and an undiscussed Level 3 change are both blocker findings.

## Layer 2 — code

[references/code-tracks.md](references/code-tracks.md): scope selection (uncommitted / staged / unpushed / branch / worktree / commit / PR), six tracks only, size-based subagent tiering, finding filters, output format. Style, naming, formatting, and refactor taste are out of scope everywhere.

## Output

Compliance verdicts first (PASS / FAIL per layer, the violated record named as R# / DEC# / ADR), then the code review in the standard format from code-tracks.

Fix offers come after the full text, each naming its mode: code for direct fixes, debug for investigate-first issues, orchestrator for 5+ mixed issues needing a planned repair. After an explicit fix request: fix only the reviewed findings, in scope, then verify. No opportunistic refactors.

## Closing

APPROVE → the change ships, and `sdf-ship` closes the plan: status DONE, its Result section (MR/PR link, date, one-line outcome), and the dir moved to docs/plans/completed/ per the `sdf-doc-standards` skill. NEEDS CHANGES → set the plan's status back to IN_PROGRESS and hand the defect list to sdf-implement; no plan file moves until an approval ships.
