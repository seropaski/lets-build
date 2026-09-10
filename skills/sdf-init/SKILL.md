---
name: sdf-init
description: Set up a repository for the agent development workflow — detect the stack, create AGENTS.md and the docs knowledge tree (glossary, design, ADR, RFC, conventions, plans), and record project conventions. Run once per project; re-run to refresh after major stack changes.
---

# init

One-time setup that makes every later skill work from the repository instead of from session memory. Product: AGENTS.md at the root plus the docs/ knowledge tree, grounded in what the code proves. Checklist: [references/setup-checklist.md](references/setup-checklist.md). AGENTS.md shape: [references/agents-template.md](references/agents-template.md).

## 0. Survey

AGENTS.md already exists → this run updates in place: keep human-written sections, fix stale facts, add what is missing, report every change. Never delete human prose.

## 1. Detect the stack

Evidence only — what files prove, no guessing: package.json, tsconfig.json, next.config.*, components.json, pyproject.toml, go.mod, Cargo.toml, CI configs, .editorconfig. Record: framework + version, language, UI system, state/data handling, layering, import alias, real script names for lint/format/test/typecheck/build (invent none). No manifests at all (empty or docs-only repo) → Stack states "undetected — no manifests found"; report that the tree fills in as code lands. Something expected is missing (no typecheck, no formatter) → list it as an open gap; do not install silently.

## 2. Create the tree

Per the `sdf-doc-standards` skill: docs/glossary, docs/architecture/{adr,rfcs}, docs/design, docs/conventions, docs/plans/{active,completed}. Create what is missing, keep what exists.

## 3. Seed

Glossary: 3–5 real domain terms harvested from routes, models, UI section names — one entry per term in the sdf-doc-standards format; the human extends. Conventions stubs only where the repo already shows the rules.

## 4. Write AGENTS.md

From [references/agents-template.md](references/agents-template.md): Architecture from detection, Commands from real scripts, Conventions from the alias and layering found. Short — it loads every session.

## 5. Report

Tree (created vs existing), stack facts with the files proving them, open gaps, and what the human should fill in by hand (product context, domain terms beyond the seed, team rules).
