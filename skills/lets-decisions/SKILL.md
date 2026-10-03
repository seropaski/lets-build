---
name: lets-decisions
user-invocable: false
description: Service skill, loaded by lets-plan, lets-research, lets-implement, and lets-review; not invoked by the user. Decision levels, the question ladder, the RFC and ADR lifecycle, and epoch-based document naming.
---

# lets-decisions

The human makes every decision that the code and the docs don't already make. This skill says how to tell the two apart, how to ask, and where the answer goes. Full rules: [references/decision-rules.md](references/decision-rules.md). Formats: [references/templates.md](references/templates.md).

## Question ladder

Climb it for every open point, in order:

1. The existing code answers it. Read it and move on.
2. The request, the spec, a contract, or an ADR answers it. Take the answer from there.
3. Nothing does. Ask the human and record a Q in plan.md. Milestones that wait on it get [!].

Only step 3 is a question. A point that is cheap to undo is still asked: reversibility lowers the cost of a wrong guess, it doesn't make guessing allowed.

Ask in small batches grouped by topic. Number each question and give one or two options plus your recommendation. An architectural fork goes alone. The answer goes into plan.md word for word.

## Levels

- **L1, what the code dictates.** Variable names, how a function splits, equivalent forms. This is execution, not a decision. If two options would behave differently for the user, it is L2, whatever it looks like.
- **L2, task-scoped.** "Reuse the existing DataTable." Put it to the human with the alternatives and record a DEC that cites the answer.
- **L3, architectural.** It binds future work: a shared abstraction, a new data flow, a heavy dependency. It goes through an RFC, the human's decision, and an ADR, and the plan links the ADR.

A quick test: if a future engineer would ask "why is it built this way?", it is at least L2. If the answer limits other features, it is L3.

## RFC: a question put to the human

Draft one as soon as an L3 fork appears: the problem, the options, the trade-offs, and a recommendation that takes a side. When the human decides, write the ADR, give the RFC its final status, and link the two. When the human defers, record a BLOCKED Q and mark the milestones that depend on it [!]. When the human rejects every option but names a direction, that direction constrains the plan, and it gets its own ADR if it is L3 itself.

## ADR: a decision already made

Written when the human accepts, not before, and not after the code has quietly committed everyone to it. It holds the context, the decision, the alternatives, the consequences, and a link back to the RFC. An L3 discovery during implementation runs the same loop and adds a DEV record to the plan.

Every new RFC or ADR, and every status change, also updates the row in `rfcs/_index.md` or `adr/_index.md` (format: the `lets-doc-standards` formats reference). Before writing a new one, read the index: the question may already have an answer.

A decision that sets a rule for how code is written from now on ("all dates go through formatDate") is also a convention. Propose it for docs/conventions/ and write it only after the human approves, per `lets-doc-standards`.

## Naming

RFCs, ADRs, and task dirs get an epoch-milliseconds id. Counters collide when two people plan on two machines; millisecond timestamps practically never do.

    docs/architecture/rfcs/1786584699364-entity-reference-registry.md
    docs/architecture/adr/1786584701127-server-state-management.md
    docs/plans/active/1786584705221-orders-status-filter/

UC, DEC, DEV, and Q counters stay local to their file. How to generate the id: [references/decision-rules.md](references/decision-rules.md).
