---
name: lets-ship
description: Commit the current changes and open a merge request, with a conventional message, a secrets check, a push, and an MR via GitLab push options or a PR via gh, chosen from the origin remote. Closes the task's plan once the MR exists. Use to finish a task or checkpoint work; say "commit only" to skip the push and the MR.
disable-model-invocation: true
---

# lets-ship

The product is the working changes committed with a conventional English message and, unless the user said "commit only", pushed with an MR or PR against the default branch. Hard rules:

- Never force-push, never skip hooks (`--no-verify`), never `--amend`.
- Commit the changes as they are. Don't fix or reformat anything along the way, beyond what a hook demands.
- Never commit a file nobody accounted for.

## 0. Scope

With no arguments, the scope is every change `git status` shows. With paths, it's only those, checked against `git status`. Free text is a title or a wish for the commit message. If you can't tell which it is, stop and ask.

## 1. Safety

- If `git status --porcelain` is empty, say "nothing to ship" and stop.
- List the untracked files. Include one only after reading it (for a binary or a very large file, its name and size are enough) and only if it belongs to the change. Ask about the rest.
- Look for secrets: files such as `.env*`, `*.pem`, `*.key`, `id_rsa*`, `*credentials*`, and keys, tokens, or passwords anywhere in the diff about to be committed. If you find one, stop and show it; secrets never ship. A `.env.example` with no real values is fine.
- Unless the run is "commit only", check the branch now, before committing. On the default branch (how to find it: forge-recipes.md), propose `<type>/<kebab-slug>` and switch to it when the human agrees. If they want to stay, commit there and ask before pushing straight to the default branch; there is no MR in that case.

## 2. Message

The subject is `<type>: <summary>`. The type is `fix`, `feat`, or `chore`; use `refactor`, `docs`, `test`, or `perf` only when it's clearly more precise. The summary is English, lowercase, at most 72 characters, with no trailing period, and says what the change is for rather than listing files. Keep the user's title word for word and add the type prefix if it's missing. Add a body only when there's real content: motivation, decisions that aren't obvious, multi-part changes. Wrap it at about 72 columns. If you're unsure of the house style, check `git log --oneline -15`.

## 3. Commit

Stage exactly the accounted-for scope: `git add -A` when that's the whole tree, `git add -A -- <paths>` otherwise. Check that `git diff --cached --stat` matches the scope. Commit with the message from a quoted heredoc (`git commit -F - <<'EOF'`), so the shell expands nothing inside it.

If a hook rejects the commit, no commit was made. Fix the cause and commit again; an `--amend` here would rewrite the previous commit. If the fix would change code beyond what the hook asks for, ask first. Show `git log -1 --stat`. With "commit only", stop here.

## 4. Push and open the MR or PR

Run `git fetch origin`. If uncommitted changes remain, ask whether to ship them too or leave them on purpose. If nothing is ahead of the default branch, say "nothing to merge" and stop.

The title follows the subject rules; with several commits, it names the task they share rather than listing them. The description is one to three sentences on what and why, in the docs language from AGENTS.md, as one paragraph with no line breaks and no commit or file lists.

Pick the forge from `git remote get-url origin`: GitLab gets push options, GitHub gets `gh pr create`, and anything else (including a self-hosted host whose name says neither) means asking the human. Commands: [references/forge-recipes.md](references/forge-recipes.md). Show the MR or PR URL from the output.

- GitLab with an MR already open on the branch: push options only apply when an MR is created, so say so.
- `gh pr create` fails because a PR exists: offer `gh pr edit`.
- The push is rejected: show the output. Force-pushing is not the fix.

## 5. Close the plan

Look for an IN_REVIEW plan in docs/plans/active/ whose Branch field, or failing that its slug, matches the current branch. Skip this step for "commit only", when no plan matches, or when no MR or PR was created. Otherwise offer to close the plan, and on the human's yes:

1. In plan.md, set Status to DONE and fill in Result: the MR or PR URL, the date, and a one-line outcome.
2. Move the plan dir from docs/plans/active/ to docs/plans/completed/ with `git mv`, and update links elsewhere in docs/ that pointed at the old path.
3. Commit this as `docs: close plan <slug>` and push it to the same branch with a plain `git push`. The open MR or PR picks it up; no new one is created.

Design docs aren't edited here; lets-implement owns them. If one is out of date, report it.
