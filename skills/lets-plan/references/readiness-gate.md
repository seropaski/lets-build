# Readiness gate

Every box must pass, or the plan isn't READY.

## Coverage

- Every R# has at least one UC, one scenario, and one milestone.
- Every scenario can be run by hand. "Check that it works" is not a scenario.
- Out of scope is stated.

## The four principles

- Think before coding: nothing was assumed. Every point the request didn't state was asked and answered by the human.
- Simplicity first: no speculative features, no single-use abstractions, no flexibility nobody asked for.
- Surgical: every plan line traces to an R#, UC#, DEC#, or a human answer. No "while we're here".
- Goal-driven: every milestone has a checkable exit criterion. "Make it work" fails.

## Decisions

- Every DEC has alternatives, risks, validation, and the human's answer word for word, with its Q.
- Every L3 fork has a decided RFC, or the human's explicit deferral with its milestones marked [!].
- No Q is OPEN. A Q may be BLOCKED only because the human deferred it. The model wrote no answer itself.

## Consistency

- spec.md and plan.md link each other, the milestones cover every UC, and every skill in the skill table maps to a milestone.
- Validation uses the project's real commands by their exact names. A deliverable with no code uses manual scenarios a reviewer can follow. An invented command fails the gate.
- ADR and convention links resolve, and the domain terms the spec relies on have approved glossary entries.
- Every glossary or convention proposal has the human's answer: approved and written, or rejected. None was written without approval.
- The Branch field is filled in.
