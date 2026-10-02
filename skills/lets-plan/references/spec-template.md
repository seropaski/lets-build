# spec.md template

The spec says what to do; the plan says how. Requirements stay word for word, because the implementer reads them as the contract. The docs language comes from AGENTS.md; the default is English.

    # <Task title>

    Created: YYYY-MM-DD
    Planned in: [plan.md](./plan.md)

    ## Objective
    One paragraph: what this delivers and why it matters now.
    No solution talk; that lives in the plan.

    ## Requirements
    Verbatim from the requester, numbered R1, R2, ...; sub-items stay under
    their parent. Nothing paraphrased, nothing dropped.

    ## Use cases
    UC-01 — <verb-phrase name>
    <Actor> <does X> → <outcome>. Edge cases as bullets when the happy path
    hides them.

    ## Acceptance scenarios
    Checkable by hand; at least one per requirement and one per risky decision:

    - IF <condition / action>, THEN <observable result>.

    ## Out of scope
    Explicit boundaries: existing behavior not to touch, features
    deliberately dropped.

    ## Coverage
    | R# | UC | Scenarios | Milestone |
    Filled in while drafting. Every R# reaches a milestone through at least
    one UC and one scenario.
