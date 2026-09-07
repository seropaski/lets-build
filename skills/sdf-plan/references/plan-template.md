# plan.md template

    # <Task title>

    Status: PLANNING | READY | IN_PROGRESS | BLOCKED | IN_REVIEW | DONE
    Created: YYYY-MM-DD      Updated: YYYY-MM-DD
    Spec: [spec.md](./spec.md)

    ## Discovery
    What the code taught us: existing patterns for this kind of work,
    reusable components / hooks / helpers (paths), API contracts,
    constraints, potential problems.

    ## Prior art
    Related plans from docs/plans/: path → what we reuse (decisions,
    contracts, files) → how this task differs. None found → say so and list
    the grep terms actually used (natural and code spellings).

    ## Architecture
    Stack facts that shape the build (from AGENTS.md, proven by files).
    ADRs and RFCs this plan complies with (links). Where the new code sits
    in the project's layering.

    ## Skills
    | Skill | Milestone | Why |
    Every skill maps to work; one with no milestone is removed.

    ## Implementation strategy
    Milestone order with the dependency logic (shared → entities → features
    → pages; contracts before consumers). Each milestone states a checkable
    result.

    ## Milestones
    - [ ] M1 ...
    - [ ] M2 ...
    [ ] todo  [-] in progress  [x] done  [!] blocked

    ## Progress
    Current: <what is being worked on right now>
    Next: <the next steps, ordered>
    Blocked: <what and why> | None
    Filled by sdf-implement after every milestone.

    ## Decisions
    DEC-01 — <decision>
      Alternatives / Risks / Validation        (L2 only; see decisions skill)

    ## Deviations
    DEV-01 — <what changed vs the plan>
      Planned / Discovered / Changed / Reason / Impact     (filled by implement)

    ## Open questions
    Q-01 — <question>
      Status: OPEN | BLOCKED | RESOLVED
      Why it matters / Waiting for / Resolution

    ## Validation
    Commands from package.json (real names only) + manual scenarios per risk,
    referencing the spec's scenarios.

    ## Result
    Filled by sdf-ship at closing: MR/PR link, date, one-line outcome.
