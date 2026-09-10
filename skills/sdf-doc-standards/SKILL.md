---
name: sdf-doc-standards
description: Service skill — loaded by sdf-init, sdf-plan, sdf-research, sdf-implement, and sdf-review; not invoked by the user. The closed documentation tree, the source-of-truth map (which document answers which question), linking rules, and glossary format.
---

# doc-standards

Documentation is a knowledge graph, not a folder of files: every document answers one question and links to the ones that answer the others. If two documents state the same thing, one of them is wrong.

## The tree

    AGENTS.md                       how the agent works in this repo
    docs/
      glossary/glossary.md          what domain terms mean here
      architecture/
        adr/                        accepted decisions (epoch-id named)
        rfcs/                       decisions under discussion (epoch-id named)
      design/                       what the system does today, one file per area
      conventions/                  per-area rules (frontend.md, testing.md, ...)
      plans/
        active/<id>-<slug>/         spec.md + plan.md of running tasks
        completed/                  archived when a task reaches DONE

Task dirs: `<epoch-id>-<slug>` — the epoch id per the `sdf-decisions` naming rules, slug English kebab-case. Design files: `<area>.md`.

THE TREE IS CLOSED: documentation exists ONLY in these locations, and every document answers exactly one row of the table below. NO new directories, NO loose .md files at the repository root or beside the code, NO files in a plan dir beyond spec.md and plan.md. Nothing fits → the document is not written — ASK the human. Only sdf-init creates and extends the tree; every other skill fills the listed places. The map stays complete only while the tree stays closed.

## Source of truth

| Question | Answered by |
|---|---|
| What does a term mean here? | glossary |
| What should we do? | spec.md |
| What did we learn about the code? | Discovery in plan.md |
| How do we build it? | plan.md |
| Why is the system built this way? | ADR |
| How does the system work today? | design |
| What are we considering? | RFC |
| How does the agent behave in this repo? | AGENTS.md |
| What actually changed? | git |
| Does it work? | tests |

Copy nothing across rows — link instead.

## Linking

Relative markdown links — they must resolve in editors, on the forge, and for the agent. A plan links every ADR it depends on; the RFC ↔ ADR pair links both ways; a spec links glossary terms instead of redefining them. Terminology changed → update the glossary; links follow.

## Glossary entry

    ## <Term>
    ### Definition               what it means in THIS project
    ### Not to be confused with  the near-terms
    ### Used by                  features, pages, modules
    ### Related                  ADR / RFC / plan links

AGENTS.md records the docs language; default English. Event-driven upkeep: [maintenance.md](references/maintenance.md).
