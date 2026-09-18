---
name: sdf-init
description: Set up a repository for the agent development workflow — analyze the project (stack, structure, domain vocabulary), interview the human (product goals, users, domain areas, open gaps) in blocking batches, then write AGENTS.md, README, and the docs knowledge tree (glossary, design, ADR, RFC, conventions, plans) from the analysis plus the answers. Run once per project; re-run to refresh after major stack changes.
---

# init

One-time setup that makes every later skill work from the repository instead of from session memory. Two mandatory phases, in order: analyze the code, then interview the human — the artifacts are written from both, never from placeholders. Product: AGENTS.md and README at the root plus the docs/ knowledge tree. Checklist: [references/setup-checklist.md](references/setup-checklist.md). AGENTS.md shape: [references/agents-template.md](references/agents-template.md).

## 0. Survey

AGENTS.md already exists → this run updates in place: keep human-written sections, fix stale facts, add what is missing, report every change. Never delete human prose.

## 1. Analyze the project

Evidence only — what files prove, no guessing. Manifests and configs (package.json, tsconfig.json, next.config.*, components.json, pyproject.toml, go.mod, Cargo.toml, CI configs, .editorconfig, README, CONTRIBUTING) give: framework + version, language, UI system, state/data handling, layering, import alias, real script names for lint/format/test/typecheck/build (invent none). Then read deeper for the domain: route paths, model and schema names, API endpoints, UI section names, directory vocabulary — the raw material for the glossary, AGENTS.md, and README. No manifests at all (empty or docs-only repo) → Stack states "undetected — no manifests found". Something expected is missing (no typecheck, no formatter) → an open gap for the interview and the report; do not install silently.

## 2. Interview the human — mandatory, blocking

The analysis answers what the code proves; ONLY THE HUMAN answers what it does not. STOP after the analysis and ask, in small batches by topic:

- product — what this project is for, its goals;
- users — who uses it and how;
- domain — the areas the analysis found (name them): confirm or correct each harvested term and its meaning; what the glossary missed;
- gaps and rules — every open gap from step 1, team rules and conventions the repo does not show; whether to create a README if none exists;
- docs language, when the existing docs are mixed or absent.

Every question is grounded in the analysis ("routes /orders and /fulfillment found — is this warehouse logistics?"), numbered, with 1–2 options and a recommendation. The run WAITS for the answers before writing anything — parking a question inside a generated file for the human to answer "later" is PROHIBITED; questions are asked, not embedded. An explicit "skip" from the human is an answer: record the item as open and continue; silence is not a skip — re-ask in the next batch. Answers are recorded verbatim; they fill Product context, the glossary, conventions, and README.

## 3. Create the tree

Per the `sdf-doc-standards` skill: docs/glossary, docs/architecture/{adr,rfcs}, docs/design, docs/conventions, docs/plans/{active,completed}. Create what is missing, keep what exists.

## 4. Seed

Glossary: the confirmed harvested terms plus the ones the interview surfaced — one entry per term in the sdf-doc-standards format. Conventions: rules the repo shows plus rules the human stated; stubs only where evidence or an answer exists, no filler.

## 5. Write AGENTS.md and README

AGENTS.md from [references/agents-template.md](references/agents-template.md): Architecture from detection, Commands from real scripts, Conventions from the alias, layering, and answers, Product context from the interview verbatim — no placeholder survives. README exists → refresh only its stale or empty project-description parts from the answers, human prose untouched; no README → written only on the interview's explicit yes. Keep AGENTS.md short — it loads every session.

## 6. Report

Tree (created vs existing), stack facts with the files proving them, every interview answer and where it landed (AGENTS.md section, glossary entry, convention file, README), and the gaps the human explicitly left open.
