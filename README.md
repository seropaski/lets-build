# 🏗️ Let's Build

Engineering workflow skills for AI coding agents. Tasks run through living documents — spec, plan, ADR, RFC, design — stored in the repository itself. A new session resumes from the repo, not from chat memory.

Six public skills: init, research, plan, implement, review, ship. Four service skills carry the shared machinery.

## Install

    npx skills add seropaski/lets-build

Then run `/lets-init` once in the target repository. It analyzes the project, interviews you, and creates the AGENTS.md and docs/ tree that every other skill reads. If docs/ is already yours, `/lets-init --docs-dir lets-docs` puts the tree under another folder, and init asks on its own when it finds a docs/ with your files in it; the folder lands in AGENTS.md, so every skill reads it from there. You need git and an agent that supports skills and subagents. Claude Code reads CLAUDE.md rather than AGENTS.md, so init offers a one-line CLAUDE.md that imports it.

## The workflow

    /lets-init       once per repo — analysis + interview → AGENTS.md, README, docs tree, glossary
      ↓
    /lets-plan       <task> → spec.md + plan.md, status READY
      ↓
    /lets-implement  milestones via subagents, progress written to plan.md
      ↓
    /lets-review     spec/plan/ADR compliance + five risk checks on the code
      ↓
    /lets-ship       commit + MR/PR (GitLab or GitHub, auto-detected)

    /lets-research   any time, outside the loop — explore the code, write
                     design docs, glossary, conventions

Every transition is a human decision: the agent never rolls from planning into coding, or from coding into committing. plan.md stays the live state — ticks, deviations, blockers — so any session continues where the last one stopped:

    ## Milestones
    - [x] M1 Query hooks and fixtures
    - [-] M3 URL sync
    - [!] M5 Integration tests    Q-02 BLOCKED: statuses endpoint returns 500

## What the repository gains

    AGENTS.md                       how the agent works in this repo
    docs/
      glossary/                     the domain model: _index.md maps the domains
                                    and how they connect, one file per domain
                                    holds its terms, their purpose and relations
      conventions/                  per-area rules; _index.md says which paths each covers
      design/                       what the system does today, one file per area
      architecture/adr/             accepted decisions, with their reasons
      architecture/rfcs/            decisions under discussion
      plans/active/<id>-<slug>/     spec.md + plan.md of running tasks
      plans/completed/              archived at DONE

The tree is closed: documentation exists only in these places, and only lets-init extends it. Every folder except plans/ has an `_index.md` table of contents, and skills start their lookups there instead of reading every file. The root is `docs` unless init put the tree elsewhere (`--docs-dir lets-docs`, or your answer when `docs` was already taken); AGENTS.md records the folder, and re-running init with a new `--docs-dir` moves the whole tree after your yes.

The glossary and the conventions are yours. An agent proposes the exact text of every entry or rule, with its evidence, and writes it only after you approve that text. Subagents can't write there at all, and review flags any change that skipped your approval.

## Usage

**Set up.** `/lets-init` analyzes the project — manifests, layering, domain vocabulary from routes, models, and UI sections — then stops and interviews you in small batches: product goals, users, domains and how their terms relate, open gaps. Product answers land verbatim in AGENTS.md's Product context and the README; the glossary and conventions are drafted from the answers and written once you approve the drafts. Existing files update in place; human prose stays untouched.

**Research.** `/lets-research How does an order's status travel from the API to the UI?` — no code changes, no spec. Every claim is proven by a file path; the answer lands in docs/design/orders.md, and new terms and observed rules come to you as glossary and convention proposals. Forks become RFCs put to you with a recommendation.

**Plan.**

    > /lets-plan Add a multi-select status filter to the orders page:
      1. Filter by several statuses at once
      2. Filter state survives a reload (URL)
      3. A reset button clears the filter

Numbered items become tracked requirements. The agent explores prior plans, reusable components, and ADRs — then asks everything the request does not state, in small batches, each question with options and a recommendation. No plan reaches READY with an open question. An architectural fork becomes an RFC; you decide; an ADR records it.

**Implement.** `/lets-implement orders-status-filter` — subagents write, validate, and review each milestone; the orchestrator never edits code. Progress, deviations (DEV), and new questions (Q) land in plan.md after every milestone. A blocked question flips its milestone to [!] and stops that thread while others continue. Re-run in any session: the plan is reconciled against the worktree and work resumes. Ends IN_REVIEW.

**Review.** `/lets-review` reviews uncommitted changes; `staged`, `branch main`, or a PR number work too. Compliance comes first (spec, plan, ADRs, design docs), then five risk checks on the code: security, correctness, data and rollout, performance, and leftovers (copied or orphaned logic). Big changes get a read-only subagent per check. Style is never flagged. If the branch has no plan, the review says so up front and checks only the code. The full review comes first; then it asks which findings to fix and how (fix here, investigate first, or rework through lets-implement), and nothing changes until you answer.

**Ship.** `/lets-ship` commits and opens the MR/PR; `commit only` stops after the commit. The message is conventional, secrets are checked before anything is staged, hooks run, and the forge is detected from the remote. Once the MR exists, it offers to close the plan: status DONE, the MR link in Result, the plan dir moved to completed/, all in a second commit on the same branch.

## What this buys you

- **Sessions are disposable.** State lives in plan.md and git, so a new session, agent, or human picks it up.
- **Memory survives turnover.** ADRs keep the why, design/ the current state, the glossary the vocabulary, RFCs the rejected paths.

## Skills reference

### Public — invoked by the user

| Skill | Invoke when | Job |
|---|---|---|
| [lets-init](skills/lets-init/SKILL.md) | once per project | project analysis, blocking interview, AGENTS.md + README + docs tree, glossary |
| [lets-research](skills/lets-research/SKILL.md) | deliverable is understanding or docs | design docs, glossary, conventions — read-only toward code |
| [lets-plan](skills/lets-plan/SKILL.md) | before any non-trivial change | requirements → discovery → questions → spec.md + plan.md, READY |
| [lets-implement](skills/lets-implement/SKILL.md) | plan is READY | milestone loop via subagents, plan.md as live state |
| [lets-review](skills/lets-review/SKILL.md) | before merge | compliance + five risk checks on the code |
| [lets-ship](skills/lets-ship/SKILL.md) | closing or checkpointing | commit + MR/PR; closes the plan |

### Service — loaded by other skills

| Skill | Loaded by | Job |
|---|---|---|
| [lets-decisions](skills/lets-decisions/SKILL.md) | plan, research, implement, review | decision levels, question ladder, RFC/ADR lifecycle, epoch naming |
| [lets-doc-standards](skills/lets-doc-standards/SKILL.md) | every skill | closed docs tree with _index.md files, source-of-truth map, domain-model and convention formats, approval rule, trust rule, discovery protocol |
| [lets-orchestration](skills/lets-orchestration/SKILL.md) | plan, research, implement, review | subagent roles (explorer included), dispatch prompts, validate/review cycle |
| [lets-skill-matrix](skills/lets-skill-matrix/SKILL.md) | plan, research, implement | capability areas → installed domain skills |

## How it compares

[OpenSpec](https://github.com/Fission-AI/openspec) and [Spec Kit](https://github.com/github/spec-kit) are the best-known spec-driven toolkits. Same core idea everywhere: specify before code. The difference is what the loop covers and what stays in the repo.

| | OpenSpec | Spec Kit | This set |
|---|---|---|---|
| Lifecycle | proposal → tasks → apply → archive | specify → plan → tasks → implement | init → plan → implement → review → ship (research off-loop), to merge |
| Project memory | spec registry with requirement deltas | one "constitution" file | glossary, ADRs, RFCs, conventions, design, archived plans — linked |
| Unstated details | agent drafts them into the proposal | agent drafts them into the spec | asked in batches, answers recorded verbatim |
| Execution | one agent over a checklist | one agent over a checklist | explorer / implementer / validator / reviewer subagents, validation per dispatch |
| Review | schema validation, before code | `/analyze`, before code | after code: compliance vs spec/plan/ADR, then five risk checks on the code |
| Shipping | not covered | not covered | commit + MR/PR, GitLab or GitHub |
| Session resume | checkboxes | checkboxes | status machine, Progress, DEV/Q records, worktree reconciliation |
| Runtime deps | npm CLI | `specify` CLI + scripts | none — plain markdown |

**Where this set is stronger:**

- **Nothing is guessed.** Unstated points are asked — batched, with a recommendation — and the answers live verbatim in the plan. Both toolkits let the agent fill the gaps silently.
- **Different eyes.** The validator and the reviewer are separate subagents; in both toolkits the author ticks its own checklist.
- **Review after code, against intent.** `/analyze` runs before code exists, and nothing verifies afterwards that the diff kept its promise. Here compliance is checked first, and an undocumented deviation blocks approval.
- **The loop runs to merge.** Ship commits, opens the MR/PR, and archives the plan.
- **Zero toolchain.** Plain markdown: readable in twenty minutes, easy to adjust, nothing breaks when you switch agents.
