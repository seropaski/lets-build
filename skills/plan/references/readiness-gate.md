# Readiness gate — every box or not READY

## Coverage

- every R# has at least one UC, one scenario, and one milestone;
- every scenario is runnable by hand — "check that it works" is not a scenario;
- out of scope is stated.

## Traceability — the four binding principles

- **think before coding**: every assumption surfaced — an explicit assumption entry with how it will be verified; none hidden in the wording;
- **simplicity first**: no speculative features, no single-use abstractions, no flexibility or configurability without a requirement, no handling of impossible scenarios; a senior engineer would not call any milestone overcomplicated;
- **surgical**: every plan line traces to R# / UC# / DEC# or a human answer — no "while we're here";
- **goal-driven**: every milestone states a verifiable exit criterion; "make it work" fails the gate.

## Decisions

- every DEC has alternatives, risks, and validation; one missing → back to the question loop;
- every Level 3 fork has an RFC that is decided, or a Q record with BLOCKED — no silent forks;
- assumptions are explicit, each with how it will be verified.

## Consistency

- spec and plan link each other;
- milestones cover every UC;
- every skill in the table maps to a milestone;
- validation commands exist in package.json under those exact names — an invented command fails the gate;
- ADR links resolve; glossary terms used in the spec exist in the glossary.

## Hand-off

- on main → propose the task branch `<type>/<kebab-slug>`; refusal → proceed on main, recorded;
- all sections pass → Status: READY;
- end of the run: report READY to the human with the next command (`implement <slug>`) and stop. Never roll into implementation yourself — READY is a human gate, in this session just as in a fresh one.
