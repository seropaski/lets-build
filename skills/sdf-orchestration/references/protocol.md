# Protocol — prompts, checklists, todos

## Dispatch prompt (implementer)

    Task (from the plan, verbatim):
    - What changes: ...
    - Where: <file:line>
    - Why: <R# / UC# / DEC#>

    Context: <stack facts, touched modules, patterns, fixtures>
    Conventions: <from AGENTS.md — layers, import alias, public APIs>
    Skills to load first: <from the plan's skill table>
    Binding principles: think before coding — state assumptions first;
    simplicity first — nothing beyond the task, no speculative abstraction,
    no "improvements" of adjacent code; surgical changes — only this task's
    files; goal-driven — say how you will verify before you code.
    Protocol: anything ambiguous or missing — stop and report the question
    with 1–2 options and a recommendation. Do not guess.
    Do not: commit; touch files outside the task.
    Before reporting: run the project's checks (typecheck, lint, tests)
    and fix your own failures.
    Report: files changed; what was done; what you ran and its result; open questions.

## Validator checklist

- `git diff` touches only this task's files — anything else is a defect;
- conventions per touched file: import alias, layer boundaries, slice public APIs;
- typecheck (command from AGENTS.md);
- every scenario runnable at this point — run it; the rest go to the deferred list explicitly.

Report: verdict pass / defects, each defect as file:line + what is wrong + what was expected.

## Reviewer checklist (per milestone)

- every changed line traces to R# / UC# / DEC# — untraceable code is a defect;
- reuse-first: nothing reimplemented that the codebase already had;
- the binding principles: surgical (no edits beyond the task), simplicity first (no speculative abstraction, no "while we're here"), goal-driven (every change serves a stated criterion);
- consistency with the project's existing patterns.

Report: verdict + defects, each as file:line + problem + expected result + the record it violates.

## Todo rules

- one todo = one plan task, or a closed part of one;
- wording states a checkable result: files + scenario;
- order follows milestones and dependencies;
- no todo without a trace to a plan task — findings during work become new traced todos, not silent scope growth;
- exactly one in_progress at a time; statuses flip at the actual transition, not in batches.
