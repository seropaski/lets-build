# Compliance review

## Read

spec.md (requirements, use cases, scenarios), plan.md (strategy, milestones, DEC / DEV / Q), every linked ADR — then the diff.

## Requirement compliance

For each R#: where does the diff implement it, and which scenario proves it? Not observable → FAIL, naming the R#. Partially covered → list what is missing.

## Plan compliance

- milestones marked [x] correspond to real, complete work;
- the strategy was followed. A different approach was taken → was a DEV record written? Undocumented deviation = defect; documented deviation = check its impact statement;
- DEC decisions hold in the code. A DEC says "reuse X", the code builds Y → deviation;
- the four binding principles hold in the diff: think before coding (nothing invented beyond the spec), surgical (no edits beyond plan tasks), simplicity first (nothing speculative or single-use), goal-driven (every change serves a requirement or a decision).

## Architecture compliance

- every ADR the plan links: respected in the changed code;
- the change introduces a Level 3 pattern (a shared abstraction others must use, a new data flow) with no RFC and no ADR → blocker: route through the `sdf-decisions` skill; do not approve silently;
- AGENTS.md conventions per touched file: import alias, layer boundaries, public APIs.

## Verdicts

PASS / FAIL per layer. Every FAIL carries evidence (file:line) and the record it violates. A FAIL on any layer blocks approval regardless of what Layer 2 finds.
