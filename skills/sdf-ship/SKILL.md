---
name: sdf-ship
description: Commit the current changes and open a merge request — conventional message, secrets check, push, then MR via GitLab push options or PR via gh on GitHub, auto-detected from the origin remote. Use to close out a task or checkpoint work. Say "commit only" to skip push and MR.
---

# ship

Product: the working changes committed with a conventional English message and, unless the user said "commit only", pushed with an MR or PR opened against the default target. No force-push, no hook bypass (`--no-verify` banned), no empty commits, no amending rejected commits.

## 0. Scope

- no arguments → the whole working tree, message generated;
- paths listed → commit only those (verify against `git status`);
- free text → a title or wish for the message;
- unclear which is which → stop and ask.

Never fix or reformat files "along the way" — commit the changes as they are.

## 1. Safety

`git status --porcelain` empty → "nothing to ship", done. Secrets — `.env*`, `*.pem`, `*.key`, `id_rsa*`, `*credentials*`, tokens or passwords visible in the diff → stop; secrets never ship. Untracked files → read fully before deciding they belong in the commit.

## 2. Message

Subject `<type>: <summary>`:

- type: `fix` / `feat` / `chore`; `refactor`, `docs`, `test`, `perf` only when clearly more precise;
- summary: English, lowercase, ≤ 72 chars, no trailing dot — the essence of the change, not a file list;
- unsure about style → `git log --oneline -15`.

The user supplied a title → keep the text verbatim; add the type prefix if it is missing. Body only for real content — motivation, non-obvious decisions, multi-part changes: blank line after the subject, paragraphs ~72 cols, about the change only. No tooling, rules, skills, plans, or process talk.

## 3. Commit

Stage the full scope (`git add -A`) or the given paths (`git add -- <paths>`). Multi-line message via heredoc:

    git commit -m "$(cat <<'EOF'
    <subject>

    <body>
    EOF
    )"

A hook rejected the commit → fix the cause, create a NEW commit; never amend. Show `git log -1 --stat`.

"commit only" → stop here.

## 4. Forge and MR/PR

`git fetch origin`. Leftover uncommitted changes → ask: ship them too, or continue deliberately — auto-committing strays is banned.

Current branch == target → stop: propose a `<type>/<kebab-slug>` branch and moving the commits; act only on consent. No commits ahead of target (`git log origin/<target>..HEAD --oneline` empty) → "nothing to merge", stop.

Title: same rules as the commit subject; several commits → their common denominator, the task, not a list. Description: 1–3 sentences, what and why, in the project's docs language (AGENTS.md; default English). No commit lists, no file lists, no process talk — the forge renders the diff itself.

Detect the forge from `git remote get-url origin`:

- gitlab (gitlab.com or a self-hosted gitlab host) → push options, recipe in [references/forge-recipes.md](references/forge-recipes.md);
- github → `gh pr create`, recipe in [references/forge-recipes.md](references/forge-recipes.md);
- anything else → ask.

Take the MR/PR URL from the command output and show it. An MR already exists on this branch → GitLab creates no duplicate but updates nothing (push options apply at creation only) — say so. On GitHub `gh pr create` fails → offer `gh pr edit`. A rejected push → show the output; force-push is not the remedy.

## 5. Close the plan

After the MR/PR is created, check docs/plans/active/ for a plan in IN_REVIEW whose branch matches the current one. Found → offer to close it (only on the human's yes): set Status: DONE, fill its Result section (MR/PR URL, date, one-line outcome), and move `docs/plans/active/<slug>/` to docs/plans/completed/ per the `sdf-doc-standards` skill. Not found, or the human declines → leave everything as is.
