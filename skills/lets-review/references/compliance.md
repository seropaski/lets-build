# Compliance review

The project rules part runs on every review. The requirements, plan, and architecture parts run only when the change has a plan.

## Read

The convention files whose "Applies to" covers the changed files (from docs/conventions/_index.md) and the glossary domains the change touches. With a plan, also spec.md (requirements, use cases, scenarios), plan.md (strategy, milestones, DEC, DEV, Q), and every linked ADR. Then the diff.

## Project rules

- The changed code follows the cross-cutting rules in AGENTS.md and every rule in the convention files that cover it. A break is a finding. The fix changes the code, or, if the human agrees the rule is wrong, a proposed change to the convention, which is written only with their approval.
- Domain terms in the diff (models, tables, routes, UI sections) match the glossary. A new or renamed term with no entry, or code that contradicts an entry's Rules or Relations, is a finding, and its fix is a proposed glossary change for the human to approve.
- Nothing in docs/glossary/ or docs/conventions/ changed without approval. An entry in the diff with no `Approved:` date, or one this change added without a record of the human's yes (a Q in plan.md), is a blocker.

## Requirements

For each R#: where does the diff implement it, and which scenario proves it? If it can't be observed, FAIL and name the R#. If it's partly covered, list what's missing.

## Plan

- Milestones marked [x] match real, complete work.
- The strategy was followed. If a different approach was taken, check for a DEV record: an undocumented deviation is a defect; a documented one gets its impact statement checked.
- DEC decisions hold in the code. A DEC that says "reuse X" while the code builds Y is a deviation.
- A decision visible in the diff with no DEC, Q, ADR, or DEV behind it is a blocker. It becomes a question for the human, per the `lets-decisions` ladder.
- The four principles hold in the diff: think before coding (nothing invented beyond the spec), surgical (no edits beyond the plan's tasks), simplicity first (nothing speculative or single-use), goal-driven (every change serves a requirement or a decision).

## Architecture

- Every ADR the plan links is respected in the changed code.
- An L3 pattern with no RFC and no ADR (a shared abstraction others must use, a new data flow) is a blocker; never approve it silently.
- The design docs of the touched areas still match what the diff does. Drift is a finding, and its fix updates the doc.

## Verdicts

PASS or FAIL for project rules and, with a plan, for requirements, plan, and architecture. Every FAIL carries file:line evidence and the record it violates. Any FAIL means "needs changes", whatever the code checks find.
