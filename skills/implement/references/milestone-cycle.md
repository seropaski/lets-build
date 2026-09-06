# Milestone cycle

## Mini-plan — before every milestone, in working notes, never skipped

Files to touch; dispatch order — tasks parallelized as far as disjoint file sets and closed dependencies allow; which skills each implementer loads; what validation covers (typecheck + which scenarios become runnable); the milestone's exit criteria.

## Dispatch — implementer

One plan task per dispatch; a task too big to review in one diff gets split into closed parts. Prompt per the `orchestration` skill's dispatch template: scope verbatim (What / Where / Why with R# / UC# / DEC# trace), context, conventions, skills, protocol, bans, report format.

## Validate — after every implementer dispatch

A fresh validator agent checks:

- `git diff` touches only this task's files — anything else is a defect;
- conventions per touched file: import alias, layer boundaries, slice public APIs;
- typecheck (command from AGENTS.md);
- every scenario runnable at this point — run it; the rest go to the deferred list explicitly.

Verdict: pass, or defects as file:line + what is wrong + what was expected. Defects → the todo stays open.

## Review — after the milestone's tasks validate clean

A fresh reviewer agent reads the stage diff against the plan:

- every changed line traces to R# / UC# / DEC# — untraceable code is a defect;
- reuse-first: nothing reimplemented that the codebase already had;
- minimalism: no speculative abstraction, no "while we're here";
- consistency with the project's patterns.

Same verdict format.

## Rework

Concrete defect list → new implementer dispatch → validator → (at stage end) reviewer. Max 2 rounds per defect. Still failing → stop: show what was tried, offer 1–2 fixes with a recommendation. Never "try harder".

## Accept

Clean verdicts + the milestone's scenarios pass → tick the milestone, update Progress (Current / Next), report to the human in two or three sentences, take the next milestone.

## Deferred list

Scenarios whose code comes later are recorded with the milestone that unlocks them. The final gate refuses to pass while this list is non-empty.
