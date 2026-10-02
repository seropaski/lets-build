# Decision rules

## When an RFC is needed

Any one of these is enough:

- two or more workable architectural approaches exist;
- the choice outlives the task, and other features will have to follow it;
- undoing it after implementation costs more than deciding now;
- the ADRs say nothing about the problem, or the task conflicts with one.

Small implementation choices don't get an RFC. A rejected RFC is a normal result: it records why a path was closed.

## ADR rules

- Written only after the human explicitly accepts.
- Precise enough to build from without rereading the RFC.
- The consequences name what future work must now comply with.
- To supersede an ADR, the new one links the old one, and the old one's status becomes `Superseded by <id>`.

## Generating the id

Use the first command that works:

    node -e 'console.log(Date.now())'
    python3 -c 'import time; print(time.time_ns() // 10**6)'
    date +%s%3N        # GNU date only

Check that the result is 13 digits. BSD date on macOS doesn't support `%N` and prints something like `17909077363N` without any error.

The slug is English kebab-case of the subject. If two documents ever get the same id, git reports a filename conflict at merge time and one side regenerates, so the failure shows itself.

## Status vocabulary

- RFC: `Proposed`, then `Accepted`, `Rejected`, or `Deferred`; later possibly `Superseded by <id>`.
- ADR: `Accepted`; later possibly `Superseded by <id>`.
- Q in plan.md: `OPEN` (asked, no answer yet), `BLOCKED` (milestones wait on it, including a question the human chose to defer), `RESOLVED` (answered).
- DEC-xx records an L2 decision; DEV-xx records a deviation from the plan.
