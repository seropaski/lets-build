# Setup checklist

## 0. Survey

- AGENTS.md exists → update in place: keep human-written text (product context, team rules), fix stale stack facts, add missing sections. Report every change; never delete human prose.
- docs/ partially exists → keep it; fill gaps only.

## 1. Stack detection — evidence only

Read: package.json, tsconfig.json, next.config.*, components.json, vite/webpack config, pyproject.toml, go.mod, Cargo.toml, pom.xml / build.gradle, docker-compose*, .github/workflows/*, .editorconfig, existing AGENTS.md / README / CONTRIBUTING.

Record only what files prove:

- framework + version, language;
- UI system, state/data libraries;
- layering: feature dirs, FSD layers, whatever the paths show;
- import alias (tsconfig paths / jsconfig), relative-path policy;
- exact script names for lint, format, test, typecheck, build;
- docs language: the existing docs' language; if mixed, ask.

Expected but missing (no typecheck, no formatter) → "Open gaps" in the report. Do not install or fix silently.

## 2. Tree

Create exactly the tree the `sdf-doc-standards` skill lists (loaded with this run) — missing entries only; keep what exists. design/ stays empty: filling it is the sdf-research skill's job.

## 3. Glossary seed

Harvest 3–5 real domain terms: route paths, model names, UI section names. One entry per term, doc-standards format (Definition / Not to be confused with / Used by / Related). The human extends from here.

## 4. Conventions stubs

Write `docs/conventions/<area>.md` only where the repo already shows rules worth recording (imports, test layout). No evidence → skip; no filler files.

## 5. AGENTS.md

From [agents-template.md](agents-template.md). Commands: real script names only. Conventions: alias, layers, shared UI location. Aim for ≤ 80 lines.

## 6. Report

- tree: created vs already existing;
- stack facts + the files that prove each;
- open gaps;
- what needs the human: product context, domain terms beyond the seed, team rules.
