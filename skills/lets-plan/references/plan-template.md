# plan.md template

    # <Task title>

    Status: PLANNING | READY | IN_PROGRESS | BLOCKED | IN_REVIEW | DONE
    Created: YYYY-MM-DD      Updated: YYYY-MM-DD
    Branch: <type>/<slug> | <default branch> (the human's choice)
    Spec: [spec.md](./spec.md)

    ## Discovery
    What the code taught us: existing patterns for this kind of work,
    reusable components, hooks, and helpers (with paths), API contracts,
    constraints, likely problems.

    ## Prior art
    Related plans from docs/plans/: the path, what we reuse (decisions,
    contracts, files), and how this task differs. If none, say so and list
    the grep terms actually used, plain and code spellings.

    ## Architecture
    Stack facts that shape the build (from AGENTS.md, proven by files).
    Links to the ADRs and RFCs this plan complies with, and to the
    convention files whose "Applies to" covers the touched code. Where the
    new code sits in the project's layering.

    ## Skills
    | Skill | Milestone | Why |
    Every skill maps to work; a skill with no milestone is removed.

    ## Implementation strategy
    The milestone order and the reason for it: shared code before entities,
    entities before features, features before pages, contracts before their
    consumers. Each milestone states a checkable result.

    ## Milestones
    - [ ] M1 ...
    - [ ] M2 ...
    [ ] todo  [-] in progress  [x] done  [!] blocked (names its Q)

    ## Progress
    Current: <what is being worked on now>
    Next: <the next steps, in order>
    Blocked: <what and why> | None
    Deferred scenarios: <scenario, unlocked by M#> | None
    Filled in by lets-implement after every milestone.

    ## Decisions
    DEC-01 — <decision>
      Answer: <the human's choice, verbatim> (Q-xx)
      Alternatives / Risks / Validation        (format: lets-decisions)

    ## Deviations
    DEV-01 — <what changed vs the plan>
      Planned / Discovered / Changed / Reason / Impact     (filled in by lets-implement)

    ## Open questions
    Q-01 — <question>
      Status: OPEN | BLOCKED | RESOLVED
      Why it matters / Waiting for / Resolution
    At READY nothing is OPEN. BLOCKED is allowed only for a question the
    human chose to defer; its milestones are marked [!] from the start.

    ## Validation
    The project's commands by their real names, plus manual scenarios per
    risk, pointing at the spec's scenarios.

    ## Result
    Filled in by lets-ship when closing: MR/PR link, date, one-line outcome.
