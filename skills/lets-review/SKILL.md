---
name: lets-review
description: Review a change before it merges. First checks it against the task's spec, plan, and ADRs, then looks for real risks in the code (security holes, wrong behavior, unsafe data changes, slow paths, logic it duplicated or left behind). Reports first and changes nothing until the human chooses what to fix. Takes an optional scope (staged, unpushed, branch, a commit, or a PR) and by default reviews the uncommitted changes.
---

# lets-review

Review reads and reports. It changes nothing, plan.md included, until the human has seen the whole report and said what to fix. A finding has to earn its place: it points at a line this change touched and names what will actually go wrong. A short report with three real problems beats a long one with ten maybes.

## 1. Which plan the change belongs to

Look for the active plan whose Branch field names the current branch. Failing that, look for one whose dir slug matches the branch name, ignoring the epoch prefix. If you find one, read its spec.md, plan.md, the ADRs it links, and the design docs of the areas the change touches. If you don't, say at the top that this change has no plan, list the active plans in case one was meant, and review the code only.

## 2. Does the change keep its promises?

[references/compliance.md](references/compliance.md). Every review checks the project rules: the conventions that cover the changed files, and the glossary for the domain terms they use. With a plan, requirements, plan, and architecture are checked too. Each part gets PASS or FAIL with evidence. These always block: a deviation with no DEV record, an architectural change nobody discussed, a decision in the code that no DEC, Q, ADR, or DEV explains, a design doc the change made untrue, and a glossary or convention change the human didn't approve.

## 3. What can go wrong in the code?

[references/code-checks.md](references/code-checks.md) says what to review, how to stay safe while doing it, the five risk checks, when to use subagents, and what the report looks like. Style, naming, formatting, and taste are never findings.

## 4. Ask what to fix

If the report has no findings, it ends with the verdict and you're done. Otherwise it ends with a question. An offer like "I can fix these if you like" is easy to skip, so ask outright:

1. Which findings to fix: all, some by number, or none.
2. How:
   - **fix here**: for a few clear findings;
   - **investigate first**: when the cause isn't obvious yet (a race, a flaky failure), find it before touching anything;
   - **rework**: write the findings into plan.md as rework and run `lets-implement`. This is the usual choice when the change has a plan, or when there are five or more findings of different kinds.

Say which answer you'd pick and why, based on how serious the findings are. Then wait.

## 5. After the answer

Fix only what the human picked, only inside the reviewed change, and run the project's checks afterwards. Nothing else gets tidied up along the way. A fix that changes the glossary or a convention is shown as exact text and written only after the human approves it.

- Fix here, or investigate first: do it in this session. If the change has a plan, add a DEV record for each fix.
- Rework: add the findings to plan.md Progress, set the status to IN_PROGRESS, and stop. The human starts `lets-implement`.

When the verdict is "ready to ship", plan.md stays as it is. The human runs `lets-ship`, which closes the plan.
