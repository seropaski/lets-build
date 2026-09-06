---
name: doc-standards
description: Service skill — loaded by the init, plan, implement, and review skills; not invoked by the user. The project knowledge tree, the source-of-truth map (which document answers which question), linking rules, glossary format, and document maintenance.
---

# doc-standards

Documentation here is a knowledge graph, not a folder of files. Every document answers one question and links to the documents that answer the others. If two documents state the same thing, one of them is wrong.

## The tree

Created by init, governed here:

    AGENTS.md                       how the agent works in this repo
    docs/
      glossary/glossary.md          what domain terms mean here
      architecture/
        adr/                        decisions made (epoch-id named, see decisions skill)
        rfcs/                       decisions being discussed (epoch-id named)
      conventions/                  per-area rules (frontend.md, testing.md, ...)
      plans/
        active/<task-slug>/         spec.md + plan.md of running tasks
        completed/                  moved here when a task reaches DONE

Task slug: English kebab-case of the task subject.

## Source of truth

| Question | Answered by |
|---|---|
| What does a term mean here? | glossary |
| What should we do? | spec.md |
| What did we learn about the code? | Discovery in plan.md |
| How do we build it? | plan.md |
| Why is the system built this way? | ADR |
| What are we considering? | RFC |
| How does the agent behave in this repo? | AGENTS.md |
| What actually changed? | git |
| Does it work? | tests |

Copy nothing across rows. Link instead.

## Linking rules

- relative markdown links — they must resolve in editors, on the forge, and for the agent;
- a plan links every ADR it depends on; the RFC ↔ ADR pair links both ways (Origin);
- a spec links glossary terms instead of redefining them;
- terminology changed → update the glossary, links follow;
- a document that nothing links to and that answers no row above should probably not exist.

## Glossary entry format

    ## <Term>
    ### Definition
    What it means in THIS project, not in general.
    ### Not to be confused with
    The near-terms (Registry vs Entity Reference Registry).
    ### Used by
    Features, pages, modules.
    ### Related
    ADR / RFC / plan links.

Domain words are overloaded in every real project. The glossary pins the local meaning so the agent stops re-asking what "registry" means in this codebase.

## Language

AGENTS.md records the project's documentation language; default English. Code identifiers, commands, and paths stay as written.

Event-driven upkeep: [maintenance.md](references/maintenance.md).
