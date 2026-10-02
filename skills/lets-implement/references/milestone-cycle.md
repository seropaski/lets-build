# Milestone cycle

## Mini-plan

Before every milestone, write in your working notes: the files to touch; the dispatch order, parallel as far as disjoint file sets and finished dependencies allow; which skills each implementer loads; what validation covers (typecheck, and which scenarios become runnable); and the milestone's exit criteria. Never skip it.

## Dispatch

One plan task per implementer. A task too big to review as a single diff is split into closed parts. Build the prompt from the `sdf-orchestration` dispatch template. Give each implementer the convention files whose "Applies to" covers its files, and the glossary domains its terms belong to. If the milestone changes how an area behaves, updating docs/design/<area>.md and its index row is part of that milestone's task. Glossary and convention changes are not: the implementer proposes them and the orchestrator takes them to the human.

## Validate, review, rework

After every implementer dispatch, a fresh validator runs the validator checklist from `sdf-orchestration`. Once all the milestone's tasks validate clean, a fresh reviewer runs the reviewer checklist on the milestone's diff. A defect keeps its todo open.

For rework, the concrete defect list goes to a new implementer dispatch, then the validator, then, at the end of the milestone, the reviewer again. Each defect gets two rounds at most. If it still fails, stop, show what was tried, and offer one or two fixes with a recommendation.

## Accept

When the verdicts are clean and the milestone's scenarios pass, tick the milestone, update Progress (Current, Next), tell the human what was done in two or three sentences, and take the next milestone.

## Deferred scenarios

A scenario whose code arrives in a later milestone is written to Deferred scenarios in plan.md's Progress, together with the milestone that unlocks it. When that milestone is done, run the scenario and take it off the list. The final gate doesn't pass while the list has entries.
