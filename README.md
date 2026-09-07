# seropaski/skills

Engineering workflow skills for AI coding agents. A task is planned, implemented, reviewed, and shipped through living documents (spec, plan, ADR, RFC) stored in the target repository itself, so any new session resumes from the repo, not from chat memory.

Five public skills cover the life of a task; four service skills carry the shared machinery. The agent reads its rules from the project's AGENTS.md, plans against the project's own knowledge tree, and writes progress back as it works.

## Install

    npx skills add seropaski/skills

The command installs the skills into your agent's skills directory. Skills reference each other by name, so no path configuration is needed; copying the directories there manually works just as well.

Installation completes inside the target repository — run `init` there once:

    > init

It creates the project's AGENTS.md and the docs/ knowledge tree and seeds the glossary, which every other skill reads. Without this step the workflow has no project knowledge to plan against.

Requirements: an agent that supports skills and subagent spawning (implement and review raise subagents for every role), and git in the target repository.

## Quick start

    init                          once per repo: AGENTS.md + docs/ tree
    plan <task>                   spec.md + plan.md, status READY
    implement <slug>              milestones, progress written back to plan.md
    review                        compliance + code review of the diff
    ship                          commit + MR/PR

Every transition below is a human decision: the agent never rolls from planning into coding, or from coding into committing, by itself.

## The workflow

    init        once per repo — AGENTS.md, docs tree, glossary seed
      ↓
    plan        <task>  →  spec.md + plan.md, status READY
                architectural forks go RFC → human decision → ADR
      ↓
    implement   milestones through subagents; progress, deviations,
                and blockers written back to plan.md
      ↓
    review      spec/plan/ADR compliance + six-track code review
      ↓
    ship        commit + MR/PR (GitLab or GitHub, auto-detected)

A plan is a living document. During implementation the agent ticks milestones and records deviations and blockers in it, so any later session continues from that state:

    ## Milestones
    - [x] M1 Query hooks and fixtures
    - [x] M2 Filter UI
    - [-] M3 URL sync
    - [ ] M4 Reset action
    - [!] M5 Integration tests        Q-02 BLOCKED: statuses endpoint returns 500

## Usage examples

### Set up a repository

    > init

The agent detects the stack from manifests, creates AGENTS.md and the docs/ tree (glossary, architecture/adr, architecture/rfcs, conventions, plans/active, plans/completed), seeds the glossary with real domain terms from the code, and reports what it changed and what the human should fill in by hand. An existing AGENTS.md and docs/ are updated in place, never overwritten; human-written sections stay untouched. Re-run after a major stack change.

### Plan a feature

    > plan Add a multi-select status filter to the orders page:
      1. Filter by several statuses at once
      2. Filter state survives a page reload (URL)
      3. A reset button clears the filter
      Materials: GET /orders?statuses=..., Figma board FGM-123
      Do not touch: the existing date-range filter

The numbered items become tracked requirements; unnumbered text becomes one requirement. The agent explores the codebase for prior plans, reusable components, and relevant ADRs, asks material questions one at a time (data contracts, edge cases, scope), records every answer verbatim, then writes spec.md (requirements, use cases, acceptance scenarios) and plan.md (discovery, architecture, milestones). The run ends with status READY and a branch suggestion, and the agent stops: no code is written until you say so.

If the task hides an architectural fork (say, a shared filter abstraction other registries would have to adopt), the agent drafts an RFC with options and a recommendation before asking. You decide; the decision is recorded as an ADR and the plan references it. A deferred decision leaves the plan BLOCKED, not guessed.

### Implement a plan

    > implement orders-status-filter

A bare `implement` also works when exactly one plan is READY or in progress. The agent orchestrates subagents: one writes, another validates the result, a third reviews the milestone. It never edits code itself. After every milestone the plan is updated: ticks, progress, deviations, new questions. A blocked question flips the plan to BLOCKED and stops that thread while independent milestones continue. The run ends IN_REVIEW.

### Resume interrupted work

    > implement orders-status-filter       # any time, in any session

State lives in plan.md and git, not in the chat. The agent reconciles the plan against the actual worktree, corrects it if reality diverged, and continues at the first unfinished milestone.

### Review changes

    > review                # uncommitted changes (the default)
    > review staged         # only what is staged
    > review branch main    # the whole branch against main
    > review 1834           # a pull request

Two layers. Compliance first: does the change match its spec, plan, and ADRs. Then code: six tracks (security, performance, business logic, deploy safety, duplication, dead code), sized to the diff, run by research subagents on larger changes. Style and taste are never flagged. The review is advisory: findings first, fixes only on your request.

### Commit and open an MR

    > ship                              # commit + push + MR/PR
    > ship commit only                  # just the commit
    > ship fix: reject empty payloads   # commit with a given subject

Conventional message, secrets checked before staging, hooks respected. GitLab gets push options, GitHub gets gh — detected from the origin remote.

## Scenarios

**A feature with a clear spec.** plan, two or three questions, READY. You skim the plan, say go, implement runs the milestones with validation after every step, review approves, ship opens the MR. Code exists only under an approved plan, and every requirement carries a manually checkable scenario.

**An architectural fork.** plan detects that a choice outlives the task, drafts an RFC, you pick, an ADR records it. The next task touching that area inherits the decision instead of re-arguing it.

**Interrupted work.** The session died mid-milestone. New session, same command: the plan says where things stand, git shows what actually happened, the agent reconciles the two and continues. Nothing lives only in chat history.

**Blocked mid-implementation.** A missing API detail stops one thread: its milestone flips to [!] with a Q record naming what is awaited, and independent milestones keep moving; the plan itself goes BLOCKED only when nothing can move. The unblock is one answer away — give it in the same or a fresh session, and implement records it and resumes.

**A drive-by change.** Small fix, no plan. Edit, review (the review states that no plan applies and checks code only), ship. The compliance layer is absent by design, not faked.

## What this buys you

- **Sessions are disposable.** The repository holds the task state. A new session, a different agent, or a human picks up from plan.md and git.
- **No code without an approved plan.** Every change traces to a requirement, a use case, or a recorded answer. Speculative work fails the readiness gate and the review.
- **Decisions survive turnover.** ADRs keep the why, the glossary keeps the vocabulary, RFCs keep rejected paths with their reasons. The agent stops re-asking what the domain terms mean in this codebase.
- **Verification is continuous.** An independent subagent validates every change; acceptance scenarios are runnable by hand; the final gate refuses to close while any scenario went unrun.
- **Review checks more than code.** Requirement, plan, and architecture compliance come before the code tracks, so a technically clean diff that betrays the plan still fails.
- **The human keeps the decisions that matter.** Architecture goes RFC → human → ADR. Research, implementation, validation, and review are the agent's job.

## Skills reference

### Public — invoked by the user

| Skill | Invoke when | Job |
|---|---|---|
| [init](skills/init/SKILL.md) | once per project, and on major stack changes | detect the stack, create AGENTS.md + docs/ knowledge tree, seed the glossary |
| [plan](skills/plan/SKILL.md) | before implementing anything non-trivial | requirements → discovery → spec.md + plan.md; RFC/ADR for architectural forks |
| [implement](skills/implement/SKILL.md) | after a plan is READY | milestone loop via subagents; plan.md stays the live state |
| [review](skills/review/SKILL.md) | before merge | compliance (spec/plan/ADR) + code review |
| [ship](skills/ship/SKILL.md) | closing a task or checkpointing work | commit + MR/PR; "commit only" skips the forge |

### Service — invoked by models, not by the user

| Skill | Loaded by | Job |
|---|---|---|
| [decisions](skills/decisions/SKILL.md) | plan, implement, review | decision levels, question ladder, RFC/ADR lifecycle, epoch-based naming |
| [doc-standards](skills/doc-standards/SKILL.md) | init, plan, implement, review | knowledge tree, source-of-truth map, linking rules, glossary format |
| [orchestration](skills/orchestration/SKILL.md) | implement, review | subagent roles, dispatch prompts, validate/review cycle |
| [skill-matrix](skills/skill-matrix/SKILL.md) | plan, implement | capability areas → domain skills installed on this machine |

## How it compares

[OpenSpec](https://github.com/Fission-AI/openspec) and [Spec Kit](https://github.com/github/spec-kit) are the two best-known spec-driven toolkits, and all three share the same core idea: specify before code. They differ in how much of the task lifecycle they cover and what stays in the repository afterwards.

| | OpenSpec | Spec Kit | This set |
|---|---|---|---|
| Lifecycle | proposal → tasks → apply → archive | specify → plan → tasks → implement | init → plan → implement → review → ship, through to merge |
| Project memory | product spec registry with requirement deltas | one static "constitution" file | glossary, ADRs, RFCs, conventions, archived plans — linked |
| Execution | one agent over a checklist | one agent over a checklist | writer, validator, and reviewer are separate subagents; validation after every dispatch |
| Review | document schema validation | `/analyze`, before code | after code: spec/plan/ADR compliance, then six code tracks |
| Shipping | not covered | not covered | commit + MR/PR, GitLab or GitHub |
| Session resume | checkboxes | checkboxes | plan status machine, Progress, DEV/Q records, plan-vs-worktree reconciliation |
| Runtime deps | npm CLI | `specify` CLI + project scripts | none, plain markdown |

**Where this set is stronger:**

- **Code checked by different eyes.** In both toolkits the agent that wrote the code also ticks its own checklist. Here the validator and the reviewer are always separate subagents; they can block a milestone, and "no finding beats a weak finding" keeps the review signal clean.
- **Decisions survive the task.** A Level 3 fork becomes an RFC, goes to the human, and lands as an ADR the plan links to; the glossary pins what domain terms mean. Neither alternative answers "why is it built this way" six months later.
- **Review against intent.** `/analyze` runs before code exists. Nothing in either toolkit verifies afterwards that the diff kept its promise; here compliance with spec, plan, and ADRs is checked first, and an undocumented deviation blocks approval.
- **The loop runs to merge.** Both stop at "the code is written". Here review hands over to ship: commit, MR/PR, plan archived to completed/.
- **Zero toolchain.** Spec Kit scaffolds helper scripts into your project; OpenSpec ships a CLI. This set is plain markdown: readable in twenty minutes, easy to adjust, indifferent to GitLab vs GitHub, and nothing breaks when you switch agents.

**One real gap:** OpenSpec's product spec registry — `specs/` with requirement deltas — accumulates a per-capability description of what the product does today. This set has no equivalent: ADRs keep the why, the glossary keeps the vocabulary, and behavior truth lives in code and tests. For contract-heavy products that registry is a loss.

The gap is also the easiest one to fill, because the two tools compose. OpenSpec is a documentation layer: what the product does today, capability by capability. This set is the development loop on top of the repository: plan, build, review, ship. Together, OpenSpec's `specs/` joins the doc-standards source-of-truth map, the plan reads it as first-class input during discovery, and ship's closing step offers to update the requirement deltas. One rule keeps them out of each other's way: this set's plan/implement drives the task loop, and `openspec/` is treated as documentation, not as a second workflow.

Pick by the gap: execution discipline, review against intent, and decision memory are covered here. Agent coverage is Spec Kit's and OpenSpec's game. A product spec registry is one OpenSpec install away — alongside, not instead.
