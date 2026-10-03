---
name: lets-research
description: Explore a codebase and record what was learned in the project's docs tree, as current-state design docs, glossary entries, and conventions. Never changes code and writes no spec, plan, or decisions. Use when the deliverable is understanding or documentation ("how does X work", "what is the state of Y", "document this area") rather than a working feature.
---

# lets-research

You're an investigator, and the product is knowledge that lasts: checked against the files, linked, and true on the day it's written. Code is read, never changed. If the request is really a feature ("research how we should add X"), say so and point to `lets-plan`; this skill records what is, not what to build.

## 0. Intake

If the request is empty or vague, propose one to three concrete research questions and let the human pick. A research question is one sentence the code can answer. Unrelated questions go to separate runs.

## 1. Ground and explore

Read AGENTS.md; if it's missing, stop and suggest `/lets-init`. Load `lets-doc-standards` and run its discovery protocol (references/discovery.md) for the areas under study. Match the areas to installed skills per `lets-skill-matrix`; an architecture or layering skill shapes how a design doc describes boundaries. For medium studies and up, send explorer subagents out in parallel (`lets-orchestration`). Verify every claim the user makes; if the code disagrees, stop and show both sides. When the code and the docs don't answer something, ask the human, per the `lets-decisions` question ladder.

## 2. Write into the tree

Documents go only where `lets-doc-standards` lists:

- how an area works today: `docs/design/<area>.md` and its index row, every claim backed by a file path, described as built, never as wished;
- a domain term, what it means, why it exists, and how it relates to others: a proposed glossary entry;
- a rule the code already follows: a proposed `docs/conventions/<area>.md` rule.

Glossary and convention proposals are written only after the human approves the exact text (`lets-doc-standards`). Show them together at the end of the study, each numbered, with its evidence. Nothing else is written: no new directories, no spec.md or plan.md. If a finding fits none of these, mention it to the human and move on. A claim you can't prove from a file is dropped, not written.

## 3. Forks go to the human

Research surfaces forks and never settles them. For an L3 fork (`lets-decisions`), draft an RFC and put it to the human with a recommendation. Don't present today's design as the only possible one.

## 4. Report and hand off

Report the questions studied, what you learned, the documents written, the glossary and convention proposals with the human's answer to each, the claims that failed verification, and the RFCs raised. Then ask one question: answer the RFCs, plan a task (`lets-plan <task>`), or stop. Research never rolls into implementation.
