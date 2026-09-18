# Setup checklist

## 0. Survey

- AGENTS.md exists → update in place: keep human-written text (product context, team rules), fix stale stack facts, add missing sections. Report every change; never delete human prose.
- docs/ partially exists → keep it; fill gaps only.

## 1. Project analysis — evidence only

Read: package.json, tsconfig.json, next.config.*, components.json, vite/webpack config, pyproject.toml, go.mod, Cargo.toml, pom.xml / build.gradle, docker-compose*, .github/workflows/*, .editorconfig, existing AGENTS.md / README / CONTRIBUTING.

Record only what files prove:

- framework + version, language;
- UI system, state/data libraries;
- layering: feature dirs, FSD layers, whatever the paths show;
- import alias (tsconfig paths / jsconfig), relative-path policy;
- exact script names for lint, format, test, typecheck, build;
- domain vocabulary: route paths, model/schema names, API endpoints, UI section names, directory names — the raw material for the glossary, AGENTS.md, and README;
- docs language: the existing docs' language.

Expected but missing (no typecheck, no formatter) → an open gap for the interview and the report. Do not install or fix silently.

## 2. Interview — mandatory, blocking

STOP after the analysis; nothing is written until the batches are answered. Small batches by topic, every question grounded in the analysis, numbered, with 1–2 options and a recommendation:

- product: purpose, goals;
- users: who uses it, how;
- domain: confirm or correct each harvested term's meaning; what the analysis missed;
- gaps and rules: the open gaps from step 1, team rules the repo does not show; create a README if none exists?
- docs language when mixed or absent.

Parking a question inside a generated file for the human to answer "later" is PROHIBITED — questions are asked, not embedded. An explicit "skip" → record the item open and move on; silence → re-ask in the next batch. Answers verbatim: they fill Product context, the glossary, conventions, and README.

## 3. Tree

Create exactly the tree the `sdf-doc-standards` skill lists (loaded with this run) — missing entries only; keep what exists. design/ stays empty: filling it is the sdf-research skill's job.

## 4. Glossary seed

The confirmed harvested terms plus the terms the interview surfaced. One entry per term, doc-standards format (Definition / Not to be confused with / Used by / Related). The human extends from here.

## 5. Conventions

`docs/conventions/<area>.md` where the repo shows rules or the human stated them. No evidence and no answer → skip; no filler files.

## 6. AGENTS.md and README

AGENTS.md from [agents-template.md](agents-template.md). Commands: real script names only. Conventions: alias, layers, shared UI location, human-stated rules. Product context: the interview answers verbatim — no placeholder survives. README exists → refresh only stale or empty description parts from the answers, human prose untouched; README requested in the interview → write it from the answers. Aim AGENTS.md for ≤ 80 lines.

## 7. Report

- tree: created vs already existing;
- stack facts + the files that prove each;
- the interview: each answer and where it landed;
- open gaps the human explicitly skipped.
