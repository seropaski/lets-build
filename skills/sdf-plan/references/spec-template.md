# spec.md template

The spec says what to do. The plan says how. Requirements stay verbatim — the implementer reads them as the contract. Docs language comes from AGENTS.md, default English.

    # <Task title>

    Created: YYYY-MM-DD
    Planned in: [plan.md](./plan.md)

    ## Objective
    One paragraph: what this delivers and why it matters now.
    No solution talk — that lives in the plan.

    ## Requirements
    Verbatim from the requester, numbered R1, R2, ...; sub-items stay under
    their parent. Nothing paraphrased, nothing dropped.

    ## Use cases
    UC-01 — <verb-phrase name>
    <Actor> <does X> → <outcome>. Edge cases as bullets when the happy path
    hides them.

    ## Acceptance scenarios
    Manually checkable; minimum one per requirement and one per risky decision:

    - IF <condition / action>, THEN <observable result>.

    ## Out of scope
    Explicit boundaries: pre-existing behavior not to touch, features
    consciously dropped.

    ## Coverage
    | R# | UC | Scenarios | Milestone |
    Filled during drafting; every R# must reach a milestone through at least
    one UC and one scenario.
