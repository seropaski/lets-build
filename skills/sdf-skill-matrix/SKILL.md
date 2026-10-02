---
name: sdf-skill-matrix
description: Service skill, loaded by lets-plan, lets-research, and lets-implement; not invoked by the user. Maps the task's capability areas to the domain skills actually installed in the current environment. Names no concrete skills, because every engineer's machine has a different set.
---

# sdf-skill-matrix

Engineers run this workflow on different machines, and each machine has a different set of domain skills. So this skill names none. It defines capability areas and a way to find matches; the concrete skills are resolved against the environment at planning time.

## Discovery

Before design, before code:

1. List the skills available here: the agent's skill list, or its skill search where one exists.
2. For each capability area the task touches ([references/matrix.md](references/matrix.md)), find an installed skill whose description covers it.
3. Record the matches in the plan's skill table: area, skill name, milestone. If an area has no match, go ahead without one and note the gap in the plan.
4. Load the matched skills before design, not after, because they change the design.

## Rules

- Every loaded skill maps to work. A skill with no milestone is noise; drop it.
- AGENTS.md can pin or override the matches for the project. Otherwise they are rediscovered on every plan.
- A domain skill governs the domain work it covers. It doesn't override this workflow's rules on asking, scope, commits, and review; if it conflicts with them, tell the human.
