# Formats

## Glossary: docs/glossary/_index.md

The domain map. Read it first: it tells you which domain file holds a term.

    # Glossary

    ## Domains
    | Domain | What it covers | File |
    |---|---|---|
    | Orders | what a customer buys and the order's life until delivery | [orders.md](orders.md) |

    ## How the domains connect
    - Orders uses Customer from [Accounts](accounts.md#customer).
    - Fulfillment starts from an Order once it's paid.

    ## Terms
    | Term | Domain | In one line |
    |---|---|---|
    | [Order](orders.md#order) | Orders | one customer purchase, from cart to delivery |

## Glossary: docs/glossary/<domain>.md

One file per domain. A term lives in exactly one domain; other domains link to it.

    # <Domain>

    What this part of the business does and why it exists, in one paragraph.
    Back to the [glossary index](_index.md).

    ## <Term>
    Definition: what it means in THIS project.
    Purpose: why it exists, what job it does for the user or the system.
    Relations:
    - <Term> <verb> <Term> (how many, required or not); link terms from other domains
    Lifecycle: <its states and what moves it between them> | none
    Rules: what must always be true about it.
    In code: <models, tables, routes, modules, with paths>
    Not to be confused with: <near-terms, and the difference>
    Related: <ADR, RFC, design links>
    Approved: YYYY-MM-DD

Leave out a field that has nothing to say, except Definition, Purpose, and Approved.

## Conventions: docs/conventions/_index.md

    # Conventions

    | Area | Applies to | File | In short |
    |---|---|---|---|
    | Frontend | src/app/**, src/features/** | [frontend.md](frontend.md) | FSD layers, alias imports, shared UI first |

The "Applies to" column is how a skill finds the rules for the files a task touches.

## Conventions: docs/conventions/<area>.md

    # <Area> conventions

    Applies to: <paths or globs>
    Back to the [conventions index](_index.md).

    ## <Rule name>
    Rule: what to do, or what not to do.
    Why: the reason, so the rule can be judged when a case doesn't fit.
    Example: a short snippet, or file:line of code that follows it.
    Source: <seen in code at file:line | stated by the human | DEC or ADR link>
    Approved: YYYY-MM-DD

A rule that binds architecture rather than how code is written belongs in an ADR; the convention links it.

## Design: docs/design/_index.md

    # Design

    | Area | Code it covers | File |
    |---|---|---|
    | Orders | src/features/orders/**, api/orders/** | [orders.md](orders.md) |

## Decisions: docs/architecture/adr/_index.md and rfcs/_index.md

    # ADRs

    | ADR | Title | Status | Date |
    |---|---|---|---|
    | [1786584701127](1786584701127-server-state-management.md) | Server state management | Accepted | 2026-09-14 |

    # RFCs

    | RFC | Title | Status | ADR |
    |---|---|---|---|
    | [1786584699364](1786584699364-server-state-management.md) | Server state management | Accepted | [1786584701127](../adr/1786584701127-server-state-management.md) |

The Status column mirrors the document's own Status line; change both in the same edit.
