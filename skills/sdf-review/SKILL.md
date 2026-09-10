---
name: sdf-review
description: Two-layer review of a change — compliance with the task's spec, plan, and ADRs, then a high-confidence code review across six tracks (security, performance, business logic, deploy safety, duplication, dead code). Advisory; no edits until the full review is written and the human asks for fixes. Optional input names a scope word, commit, branch, or PR; empty input reviews uncommitted changes.
---

# review

Advisory by default: the complete review first, fix offers after. Never flag outside the layers and tracks below. Prefer no finding over a weak finding.

## Layer 0 — context

Attribute the change: match the current branch's slug against the docs/plans/active/ dir names, ignoring epoch prefixes — a match names the plan. No match → a drive-by: Layer 1 does not apply — say so up front and list the active plans. Matched → read spec.md, plan.md, the linked ADRs, and the design docs of the touched areas; Layer 1 applies.

## Layer 1 — compliance

[references/compliance.md](references/compliance.md): every requirement implemented, the plan's strategy followed, ADRs respected, the four binding principles held. Blockers: an undocumented deviation, an undiscussed Level 3 change, a decision in the diff with no DEC / Q / ADR / DEV trace, a design doc the diff made untrue.

## Layer 2 — code

[references/code-tracks.md](references/code-tracks.md): scope selection, six tracks only, size-based subagent tiering, finding filters, output format. Style, naming, formatting, and refactor taste are out of scope everywhere.

## Output

Compliance verdicts first (PASS / FAIL per layer, the violated record named as R# / DEC# / ADR), then the code review in the standard format. Fix offers come after the full text, each naming its mode: code / debug / orchestrator (5+ mixed issues). After an explicit fix request: fix only the reviewed findings, in scope, then verify. No opportunistic refactors.

## Closing

APPROVE → the human ships; `sdf-ship` closes the plan (DONE, Result, archive, design docs updated). NEEDS CHANGES → status back to IN_PROGRESS, the defect list to `sdf-implement`; no plan file moves until an approval ships.
