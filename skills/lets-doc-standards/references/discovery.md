# Discovery: what the project already knows

Used by lets-plan and lets-research. Work top-down; each level either answers the question or sends you to the next one. At every level, start from the folder's `_index.md` and open only the files it points to. Grep is the fallback for what the index doesn't cover.

## 1. Glossary

Open docs/glossary/_index.md, find the domains the request touches, and read those domain files. If the request uses a term ambiguously and the glossary has no entry for it, ask the human what it means here, then propose an entry for approval (the approval rule in SKILL.md). The glossary exists so this question gets asked once per project, not once per task.

## 2. Conventions, ADRs, RFCs, design docs

- docs/conventions/_index.md: the convention files whose "Applies to" paths cover the code the task touches. Their rules bind the plan.
- docs/architecture/adr/_index.md and rfcs/_index.md: the decisions on the task's topics. If the work would break an ADR, either comply or bring the conflict to the human, spelled out. If no ADR covers the topic, note that; the gap feeds the L3 check later.
- docs/design/_index.md: the areas the task touches. Their design docs are required reading, because they say how the area works today.

## 3. Prior art

Before any new research, search docs/plans/active and docs/plans/completed for earlier work on the same problem.

1. Grep the contents first. Take the nouns from the requirements (entities, UI sections, operations) and grep plan bodies case-insensitively for at least two spellings of each: the plain term and its spelling in code (routes, models, files), plus plurals. Dir names are mostly opaque slugs, so a match in the body counts as a candidate.
2. Glob file names second, as an extra. Zero name matches proves nothing.
3. Read every candidate. With more than five, rank them by how precisely they hit the terms, then by recency from the epoch prefix. Pull out decisions, data contracts, touched files, and scenarios.

You may write "nothing found" only after grepping at least two spellings, and the Prior art section then lists them.

Reuse what was decided instead of deciding it again. An old plan that already covers part of this task gets cited, not duplicated. Current code beats old plans, so check that the old decisions survived. An old plan that contradicts this request is a question for the human.

## 4. Reuse sweep

Before designing anything new, look for what exists: similar components, hooks, filters, utils. Extending beats duplicating. For UI, check the component inventory or registry that AGENTS.md names.

## 5. Deep exploration

For medium tasks and larger, dispatch read-only explorer subagents in parallel, one per independent area: touched files, patterns, data contracts, change boundaries. The role contract is in the `lets-orchestration` skill. A small isolated edit doesn't need one.

## 6. Claim check

Verify every claim the user makes about the code ("there's already a hook for that"). If the code says otherwise, stop and show both sides.
