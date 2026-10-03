# Templates: RFC, ADR, plan records

## RFC

    # RFC <epoch-ms>: <title>

    Status: Proposed | Accepted | Rejected | Deferred | Superseded by <id>
    Date: YYYY-MM-DD

    ## Problem
    What forces a decision now. Constraints. What breaks if we do nothing.

    ## Options
    One subsection per option: the approach, what it costs, what it rules out.

    ## Trade-offs
    Compare on the axes that matter for this project: performance,
    complexity, migration cost, team familiarity. Say which axis wins.
    A fake balance is worse than a stance.

    ## Recommendation
    One option, and why. A recommendation without a stance is a defect.

    ## Decision
    Filled in after the human decides. Links the ADR.

## ADR

    # ADR <epoch-ms>: <title>

    Status: Accepted | Superseded by [ADR <id>](<id>-<slug>.md)
    Date: YYYY-MM-DD

    ## Context
    The forces at play; what the system looked like before.

    ## Decision
    What we do, in the present tense, precise enough to build from.

    ## Alternatives
    What else was on the table, and why not.

    ## Consequences
    What gets easier, what gets harder, what future work must comply with.

    ## Origin
    Discussed in [RFC <id>](../rfcs/<id>-<slug>.md)

## Plan records

    DEC-01 — <decision, one line>
      Answer: <the human's choice, verbatim> (Q-xx)
      Alternatives: <what else, and why not>
      Risks: <what may break>
      Validation: <scenario, typecheck, or manual check>

A DEC with no answer, no alternatives, or no validation isn't a decision yet. Send it back to the question ladder.

    DEV-01 — <what changed vs the plan> (YYYY-MM-DD)
      Planned / Discovered / Changed / Reason / Impact

    Q-01 — <question>
      Status: OPEN | BLOCKED | RESOLVED
      Why it matters / Waiting for / Resolution (the human's answer, verbatim)
