# Maintenance: which event updates which document

Every change to a file in a docs folder also updates that folder's `_index.md` in the same edit. Rows marked **approval** are written only after the human approves the exact text (SKILL.md).

| Event | Update | Who |
|---|---|---|
| a domain term is new, renamed, or changes meaning | its entry in docs/glossary/<domain>.md, **approval** | whichever skill found it: init, research, plan, or implement when a milestone adds or changes an entity |
| a new domain appears | a domain file and a row in the glossary map, **approval** | same |
| a rule for how code is written is seen in the code or stated by the human | docs/conventions/<area>.md, **approval** | init, research, plan (a DEC that sets a rule) |
| code breaks a convention | a review finding; the fix changes the code, or the convention with **approval** | review |
| a convention keeps being broken or binds architecture | propose an ADR | whoever notices |
| an L3 question is raised and not yet decided | an RFC with status Proposed, its index row, a Q in plan.md | plan, research, implement |
| an L3 decision is accepted | the ADR and its index row, the RFC's final status, the plan's link to the ADR | plan, implement |
| implementation deviates from the plan | a DEV record in plan.md | implement |
| a milestone is done | its tick and Progress in plan.md | implement |
| a milestone changes how an area behaves | docs/design/<area>.md and its index row, inside the same milestone | implement |
| a task reaches DONE | plan.md Status and Result; the plan dir moves to completed/, and links to the old path are updated | ship |
| the stack changes | Stack and Commands in AGENTS.md | init on a re-run |

## A document is done when

- it answers exactly one row of the table in SKILL.md;
- its index row exists and says what the file holds;
- its links are relative and resolve;
- it copies no text that lives elsewhere;
- global documents are epoch-named, and task-local counters stay inside their plan.
