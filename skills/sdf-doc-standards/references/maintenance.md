# Maintenance — event → document

| Event | Touch |
|---|---|
| new or changed domain term | glossary entry; existing links keep working |
| Level 3 decision accepted | ADR + RFC final status + plan links the ADR |
| Level 3 question raised, undecided | RFC Proposed + Q record in plan.md |
| deviation found during implement | DEV record in plan.md |
| milestone done | milestone tick + Progress (Current/Next) in plan.md |
| task DONE | plan dir active → completed, status DONE, ADRs created are linked from the plan |
| shipped task changed an area's behavior | docs/design/<area>.md updated to the new current state |
| convention drift spotted | `conventions/<area>.md`; if recurring, propose an ADR |
| stack change | AGENTS.md Stack and Commands sections |

## A document is done when

- it answers exactly one source-of-truth row (see the table in SKILL.md);
- its links are relative and resolve;
- it contains no copy of text that lives elsewhere;
- global documents are epoch-named, task-local counters stay inside their plan.
