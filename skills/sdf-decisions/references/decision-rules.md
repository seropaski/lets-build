# Decision rules

## RFC criteria — any one is enough

- two or more viable architectural approaches exist;
- the choice outlives the task: other features will have to comply;
- reversing it after implementation costs more than deciding now;
- existing ADRs are silent on the problem, or the task conflicts with one.

No RFC for small implementation choices. A rejected RFC is a normal, useful outcome — it records why a path was closed.

## ADR rules

- written only after an explicit human acceptance;
- precise enough to build from without re-reading the RFC;
- consequences name what future work must now comply with;
- superseding: the new ADR links the old one, the old ADR's status becomes `Superseded by <id>`.

## Naming

Epoch milliseconds + kebab-case slug:

    docs/architecture/adr/<id>-<slug>.md
    docs/architecture/rfc/<id>-<slug>.md

Generate `<id>` with whichever is available:

    date +%s%3N                                                # GNU/Linux
    python3 -c 'import time; print(time.time_ns() // 10**6)'   # python3
    node -e 'console.log(Date.now())'                          # node

Sequence numbers (`adr-001`) collide as soon as two people plan on two machines. Milliseconds do not, for practical purposes. If two documents ever do land on the same id, git reports the filename conflict at merge time and one side regenerates — the failure is self-reporting, not silent. Slug: English kebab-case of the subject.

## Status vocab

- RFC: `Proposed` → `Accepted` | `Rejected` | `Deferred`; later possibly `Superseded by <id>`.
- ADR: `Accepted`; later possibly `Superseded by <id>`.
- plan records: `DEC-xx` (L2 decisions), `DEV-xx` (deviations), `Q-xx` (questions, status OPEN | BLOCKED | RESOLVED).
