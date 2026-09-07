# Knowledge map — discovery protocol

Work top-down; each level either answers or sends you deeper.

## 1. Glossary

Load the terms the request uses. A term the request uses ambiguously with no glossary entry → ask the human what it means HERE, then propose the entry in the sdf-doc-standards format. The glossary exists so this question is asked once per project, not once per task.

## 2. ADR / RFC scan

grep docs/architecture/adr and rfcs for the task's entities and areas. A plan that would violate an ADR either complies or goes to the human with the conflict spelled out. No ADR on topic → note it; that silence feeds the L3 check later.

## 3. Prior art — before any new research

Search docs/plans/active and completed for earlier work on the same problem.

1. **Content grep first.** Extract the nouns from the requirements: entities, UI sections, operations. For each: grep -i over plan bodies in at least two variants, the natural-language term AND its code spelling from routes/models/files, plus plurals. A body match is a candidate even when the dir name is an opaque slug, which most are.
2. **File-name glob second**, additional only. Zero name matches proves nothing.
3. **Read every candidate.** More than five → rank by term-hit precision, then recency. Extract decisions, data contracts, touched files, scenarios.

"Nothing found" is legitimate only after at least two term variants were actually grepped — the Prior art section then lists those terms.

Rules: reuse what was decided — do not re-decide it. An old plan that already implements part of this task gets cited, not duplicated. Current code beats old plans: verify the decisions survived. An old plan contradicting this request → human question.

## 4. Reuse-first sweep

Before designing anything new, find what exists: similar components, hooks, filters, utils. Extending beats duplicating. Shared UI: check the project's component inventory or registry per AGENTS.md before writing new UI.

## 5. Deep exploration

Medium tasks and up: dispatch read-only explore subagents in parallel, one per independent area — touched files, patterns, data contracts, change boundaries; the role contract lives in the `sdf-orchestration` skill. A quick isolated edit does not need one.

## 6. Claim check

Every user claim about the code ("there's already a hook for that") gets verified. A contradiction → stop and show both sides.
