# Templates — RFC, ADR, plan records

## RFC

    # RFC <epoch-ms>: <title>

    Status: Proposed | Accepted | Rejected | Superseded by <id> | Deferred
    Date: YYYY-MM-DD

    ## Problem
    What forces a decision now. Constraints. What breaks if we do nothing.

    ## Options
    One subsection per option: the approach, what it costs, what it forecloses.

    ## Trade-offs
    Comparison on the axes that matter for this project — performance,
    complexity, migration cost, team familiarity. State which axis dominates;
    fake balance is worse than a stance.

    ## Recommendation
    One option, and why. A recommendation without a stance is a defect.

    ## Decision
    Filled after the human decides. Links the ADR.

## ADR

    # ADR <epoch-ms>: <title>

    Status: Accepted | Superseded by [ADR <id>](<id>-<slug>.md)
    Date: YYYY-MM-DD

    ## Context
    The forces at play; what the system looked like before.

    ## Decision
    What we do, in present tense, precise enough to build from.

    ## Alternatives
    What else was on the table, and why not.

    ## Consequences
    What becomes easier, what becomes harder, what future work must comply with.

    ## Origin
    Discussed in [RFC <id>](../rfcs/<id>-<slug>.md)

## Plan records

    DEC-01 — <decision, one line>
      Answer: <the human's choice, verbatim> (Q-xx)
      Alternatives: <what else, why not>
      Risks: <what may break>
      Validation: <scenario / typecheck / manual check>

A DEC without an answer, alternatives, or validation is not a made decision — return it to the question loop.

    DEV-01 — <what changed vs the plan> (YYYY-MM-DD)
      Planned / Discovered / Changed / Reason / Impact

    Q-01 — <question>
      Status: OPEN | BLOCKED | RESOLVED
      Why it matters / Waiting for / Resolution
