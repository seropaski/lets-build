---
name: skill-matrix
description: Service skill — loaded by the plan and implement skills; not invoked by the user. Maps the task's capability areas to domain skills actually installed in the current environment. Names no concrete skills, because every engineer's machine carries a different set.
---

# skill-matrix

Engineers of different specialties run this workflow on different machines, and every machine carries a different set of domain skills. This skill therefore names none. It defines capability areas and a discovery protocol; concrete matches are resolved against the environment at planning time.

## Discovery protocol — before design, before code

1. Enumerate the skills available in this environment: the agent's skill list, or its skill-search mechanism where one exists.
2. For each capability area the task touches (see [references/matrix.md](references/matrix.md)), find an installed skill whose description covers it.
3. Record the matches in the plan's skill table: area → skill name → milestone. An area with no match → proceed without it and note the gap in the plan.
4. Load matched skills before design, not after — they change the design itself.

Rules:

- a skill with no milestone attached is noise — every loaded skill maps to work;
- AGENTS.md may pin or override the matches for the project;
- with no AGENTS.md, matches are re-discovered on every plan.
