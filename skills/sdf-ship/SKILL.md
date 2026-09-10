---
name: sdf-ship
description: Commit the current changes and open a merge request — conventional message, secrets check, push, then MR via GitLab push options or PR via gh on GitHub, auto-detected from the origin remote. Use to close out a task or checkpoint work. Say "commit only" to skip push and MR.
---

# ship

Product: working changes committed with a conventional English message and, unless the user said "commit only", pushed with an MR/PR against the default target. NEVER force-push, NEVER bypass hooks (`--no-verify` banned), NEVER amend a rejected commit, NEVER auto-commit stray files. Never fix or reformat files "along the way" — commit the changes as they are.

## 0. Scope

No arguments → the whole working tree. Paths → only those (verify against `git status`). Free text → a title or wish for the message. Unclear → stop and ask.

## 1. Safety

`git status --porcelain` empty → "nothing to ship", done. Secrets — `.env*`, `*.pem`, `*.key`, `id_rsa*`, `*credentials*`, tokens or passwords visible in the diff → STOP; secrets never ship. Untracked files → read fully before including.

## 2. Message

Subject `<type>: <summary>` — type `fix` / `feat` / `chore` (`refactor`, `docs`, `test`, `perf` only when clearly more precise); summary English, lowercase, ≤ 72 chars, no trailing dot, the essence not a file list. The user's title is kept verbatim, the type prefix added if missing. Body only for real content — motivation, non-obvious decisions, multi-part changes; ~72 cols. Unsure about style → `git log --oneline -15`.

## 3. Commit

`git add -A` or the given paths; heredoc for a multi-line message. A hook rejected the commit → fix the cause, create a NEW commit. Show `git log -1 --stat`. "commit only" → stop here.

## 4. Forge

`git fetch origin`. Leftover uncommitted changes → ask: ship them too or continue deliberately. On the target branch → stop, propose `<type>/<kebab-slug>` and moving the commits, act on consent. Nothing ahead of target → "nothing to merge", stop. Title: subject rules; several commits → their common denominator, the task, not a list. Description: 1–3 sentences, what and why, in the docs language from AGENTS.md; no commit lists, no file lists.

Forge from `git remote get-url origin`: gitlab → push options; github → `gh pr create`; anything else → ask. Recipes: [references/forge-recipes.md](references/forge-recipes.md). Show the MR/PR URL from the output. An MR already exists on the branch (GitLab) → say so — push options apply at creation only. `gh pr create` failed → offer `gh pr edit`. A rejected push → show the output; force-push is not the remedy.

## 5. Close the plan

An IN_REVIEW plan in docs/plans/active/ whose branch matches the current one → offer to close it, only on the human's yes: Status DONE, Result (MR/PR URL, date, one-line outcome), move the dir to docs/plans/completed/ per the `sdf-doc-standards` skill — and update the design docs of the areas the task changed. Not found or declined → leave everything as is.
