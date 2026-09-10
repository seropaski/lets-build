# seropaski/skills

Engineering workflow skills for AI coding agents. Tasks run through living documents — spec, plan, ADR, RFC, design — stored in the repository itself. A new session resumes from the repo, not from chat memory.

Six public skills: init, research, plan, implement, review, ship. Four service skills carry the shared machinery.

## Install

    npx skills add seropaski/skills

Then run `/sdf-init` once in the target repository — it creates the AGENTS.md and docs/ tree every other skill reads. Needs an agent with skills and subagent spawning, and git.

## The workflow

    /sdf-init       once per repo — AGENTS.md, docs tree, glossary seed
      ↓
    /sdf-plan       <task> → spec.md + plan.md, status READY
      ↓
    /sdf-implement  milestones via subagents, progress written to plan.md
      ↓
    /sdf-review     spec/plan/ADR compliance + six-track code review
      ↓
    /sdf-ship       commit + MR/PR (GitLab or GitHub, auto-detected)

    /sdf-research   any time, outside the loop — explore the code, write
                    design docs, glossary, conventions

Every transition is a human decision: the agent never rolls from planning into coding, or from coding into committing. plan.md stays the live state — ticks, deviations, blockers — so any session continues where the last one stopped:

    ## Milestones
    - [x] M1 Query hooks and fixtures
    - [-] M3 URL sync
    - [!] M5 Integration tests    Q-02 BLOCKED: statuses endpoint returns 500

## What the repository gains

    AGENTS.md                       how the agent works in this repo
    docs/
      glossary/glossary.md          what domain terms mean here
      architecture/adr/             accepted decisions, with their reasons
      architecture/rfcs/            decisions under discussion
      design/                       what the system does today, one file per area
      conventions/                  per-area rules
      plans/active/<id>-<slug>/     spec.md + plan.md of running tasks
      plans/completed/              archived at DONE

The tree is closed: documentation exists only in these places, and only sdf-init extends it.

## Usage

**Set up.** `/sdf-init` detects the stack from manifests, creates the tree, seeds the glossary with real domain terms, reports the gaps. Existing files update in place; human prose stays untouched.

**Research.** `/sdf-research How does an order's status travel from the API to the UI?` — no code changes, no spec. Every claim is proven by a file path; the answer lands in docs/design/orders.md, new terms in the glossary, observed rules in conventions. Forks become RFCs put to you with a recommendation.

**Plan.**

    > /sdf-plan Add a multi-select status filter to the orders page:
      1. Filter by several statuses at once
      2. Filter state survives a reload (URL)
      3. A reset button clears the filter

Numbered items become tracked requirements. The agent explores prior plans, reusable components, and ADRs — then asks everything the request does not state, in small batches, each question with options and a recommendation. No plan reaches READY with an open question. An architectural fork becomes an RFC; you decide; an ADR records it.

**Implement.** `/sdf-implement orders-status-filter` — subagents write, validate, and review each milestone; the orchestrator never edits code. Progress, deviations (DEV), and new questions (Q) land in plan.md after every milestone. A blocked question flips its milestone to [!] and stops that thread while others continue. Re-run in any session: the plan is reconciled against the worktree and work resumes. Ends IN_REVIEW.

**Review.** `/sdf-review` reviews uncommitted changes; `staged`, `branch main`, or a PR number works too. Compliance first (spec, plan, ADRs, design docs), then six code tracks — security, performance, business logic, deploy safety, duplication, dead code — on read-only subagents. Style is never flagged. Findings first, fixes only on request. No plan on the branch → code-only review, stated up front.

**Ship.** `/sdf-ship` commits and opens the MR/PR; `commit only` stops after the commit. Conventional message, secrets checked, hooks respected, forge auto-detected. On approval it closes the plan: DONE, archive to completed/, design docs updated.

## What this buys you

- **Sessions are disposable.** State lives in plan.md and git — a new session, agent, or human picks it up.
- **Questions, not guesses.** Every unstated point is asked, batched, with options; the answer lands verbatim in the plan.
- **Memory survives turnover.** ADRs keep the why, design/ the current state, the glossary the vocabulary, RFCs the rejected paths.
- **Different eyes on every change.** A validator and a reviewer — never the author — check each dispatch and milestone.
- **The loop runs to merge.** Review checks intent before code; ship commits, opens the MR, archives the plan.

## Skills reference

### Public — invoked by the user

| Skill | Invoke when | Job |
|---|---|---|
| [sdf-init](skills/sdf-init/SKILL.md) | once per project | stack detection, AGENTS.md + docs tree, glossary seed |
| [sdf-research](skills/sdf-research/SKILL.md) | deliverable is understanding or docs | design docs, glossary, conventions — read-only toward code |
| [sdf-plan](skills/sdf-plan/SKILL.md) | before any non-trivial change | requirements → discovery → questions → spec.md + plan.md, READY |
| [sdf-implement](skills/sdf-implement/SKILL.md) | plan is READY | milestone loop via subagents, plan.md as live state |
| [sdf-review](skills/sdf-review/SKILL.md) | before merge | compliance + six-track code review |
| [sdf-ship](skills/sdf-ship/SKILL.md) | closing or checkpointing | commit + MR/PR; closes the plan |

### Service — loaded by other skills

| Skill | Loaded by | Job |
|---|---|---|
| [sdf-decisions](skills/sdf-decisions/SKILL.md) | plan, research, implement, review | decision levels, question ladder, RFC/ADR lifecycle, epoch naming |
| [sdf-doc-standards](skills/sdf-doc-standards/SKILL.md) | all of the above + init | closed docs tree, source-of-truth map, glossary format |
| [sdf-orchestration](skills/sdf-orchestration/SKILL.md) | plan, research, implement, review | subagent roles (explorer included), dispatch prompts, validate/review cycle |
| [sdf-skill-matrix](skills/sdf-skill-matrix/SKILL.md) | plan, research, implement | capability areas → installed domain skills |

## How it compares

[OpenSpec](https://github.com/Fission-AI/openspec) and [Spec Kit](https://github.com/github/spec-kit) are the best-known spec-driven toolkits. Same core idea everywhere: specify before code. The difference is what the loop covers and what stays in the repo.

| | OpenSpec | Spec Kit | This set |
|---|---|---|---|
| Lifecycle | proposal → tasks → apply → archive | specify → plan → tasks → implement | init → plan → implement → review → ship (research off-loop), to merge |
| Project memory | spec registry with requirement deltas | one "constitution" file | glossary, ADRs, RFCs, conventions, design, archived plans — linked |
| Unstated details | agent drafts them into the proposal | agent drafts them into the spec | asked in batches, answers recorded verbatim |
| Execution | one agent over a checklist | one agent over a checklist | explorer / implementer / validator / reviewer subagents, validation per dispatch |
| Review | schema validation, before code | `/analyze`, before code | after code: compliance vs spec/plan/ADR, then six code tracks |
| Shipping | not covered | not covered | commit + MR/PR, GitLab or GitHub |
| Session resume | checkboxes | checkboxes | status machine, Progress, DEV/Q records, worktree reconciliation |
| Runtime deps | npm CLI | `specify` CLI + scripts | none — plain markdown |

**Where this set is stronger:**

- **Nothing is guessed.** Unstated points are asked — batched, with a recommendation — and the answers live verbatim in the plan. Both toolkits let the agent fill the gaps silently.
- **Different eyes.** The validator and the reviewer are separate subagents; in both toolkits the author ticks its own checklist.
- **Review after code, against intent.** `/analyze` runs before code exists, and nothing verifies afterwards that the diff kept its promise. Here compliance is checked first, and an undocumented deviation blocks approval.
- **The loop runs to merge.** Ship commits, opens the MR/PR, archives the plan, updates design docs.
- **Zero toolchain.** Plain markdown: readable in twenty minutes, easy to adjust, nothing breaks when you switch agents.
