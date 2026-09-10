# AGENTS.md template

Fill every `<...>` from detection. Keep the file short — it loads in every session. The human owns the sections marked as such.

    # <Project name> — agent instructions

    ## Stack
    <framework + version, language, UI system, state/data, layering>
    Proven by: <manifest files>

    ## Commands
    - typecheck: <script>
    - lint / format: <scripts>
    - test: <script>
    - build: <script>
    Only commands the project actually defines — invented ones fail later gates.

    ## Conventions
    - imports: <alias rule, relative paths banned>
    - layers: <which code lives where; import boundaries; public API rule for cross-slice imports>
    - shared UI: <component inventory or registry to check before writing new UI>
    - docs language: <language>

    ## Before coding
    1. Read the design doc and ADRs relevant to the area (docs/design/, docs/architecture/adr/).
    2. Read the task's spec.md and plan.md.
    3. Inspect existing implementations; extend before duplicating.
    4. No new architectural pattern without an RFC.

    ## During implementation
    1. Follow layer boundaries and the import alias.
    2. Update plan.md progress after meaningful milestones.
    3. Document deviations (DEV) and blocked questions (Q) — never silently.
    4. Run typecheck, lint, and tests before handing over.

    ## Architecture decisions
    RFC when: several viable approaches / affects other features / hard to reverse /
    ADRs silent or conflicted. No RFC for small choices.
    ADR when: a decision is accepted and future work must comply with it.

    ## Workflow
    - init — project setup (this file, docs tree)
    - research — explores the code, writes current-state docs (docs/design/), glossary, conventions
    - plan — spec.md + plan.md before code
    - implement — milestone loop, writes progress back to plan.md
    - review — spec/plan/ADR compliance + code review
    - ship — commit + MR/PR

    ## Documentation rules
    Documents are linked, not duplicated: terminology → glossary,
    decisions → ADR, current behavior → design, task state → plan.md,
    changes → git. The docs tree is closed — no documents outside it.
    Link relatively. Update the source of truth, never a copy.

    ## Execution protocol
    ANY information the request does not state explicitly → ASK THE HUMAN.
    Guessing, assuming, and deciding silently are PROHIBITED — for the agent
    and every subagent. Questions come with 1–2 options and a recommendation.

    ## Product context
    <human-owned: what this product is, who uses it, domain quirks>
