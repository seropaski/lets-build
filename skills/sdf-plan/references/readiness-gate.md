# Readiness gate — every box or not READY

## Coverage

- every R# has at least one UC, one scenario, and one milestone;
- every scenario is runnable by hand — "check that it works" is not a scenario;
- out of scope is stated.

## Traceability — the four binding principles

- **think before coding**: nothing was assumed — every point the request did not state explicitly was asked and answered by the human;
- **simplicity first**: no speculative features, no single-use abstractions, no unrequested flexibility;
- **surgical**: every plan line traces to R# / UC# / DEC# or a human answer — no "while we're here";
- **goal-driven**: every milestone states a verifiable exit criterion — "make it work" fails.

## Decisions

- every DEC has alternatives, risks, validation, and the human's verbatim answer (Q trace);
- every L3 fork has a decided RFC, or the human's explicit deferral with its dependent milestones marked [!];
- every Q is RESOLVED — a deferral counts; OPEN or BLOCKED fails the gate, and the model never supplied an answer itself.

## Consistency

- spec and plan link each other; milestones cover every UC; every skill maps to a milestone;
- validation: the project's real commands by their exact names for code changes; for a codeless deliverable, manually checkable scenarios a reviewer can follow — an invented command fails the gate;
- ADR links resolve; glossary terms used in the spec exist in the glossary.

## Hand-off

- on main → propose the task branch `<type>/<kebab-slug>`; refusal recorded;
- all sections pass → Status: READY;
- report READY with the next command (`sdf-implement <slug>`) and STOP. Never roll into implementation — READY is a human gate, in this session as in a fresh one.
