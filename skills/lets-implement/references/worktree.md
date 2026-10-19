# Worktrees

## One plan, one worktree

Offer a worktree whenever a plan is about to start and this checkout is busy with something else — another plan's branch, uncommitted work — or when the human wants two tasks in parallel. The human decides; a worktree is never created silently. Nothing below happens without their yes.

## Create

    git fetch origin
    git worktree add -b <type>/<slug> ../<repo>-<slug> origin/<default>

The branch already exists (the plan records it): `git worktree add ../<repo>-<slug> <branch>`. With no remote, base the new branch on the local default branch. A sibling directory, never a folder inside the repository: nothing to gitignore, and the main checkout stays the main checkout.

Then move the plan across. It is untracked at this point, so a plain move changes nothing in git; if it was committed on the base branch, the fresh worktree already has it and there is nothing to move.

    mkdir -p ../<repo>-<slug>/<docs-root>/plans/active
    mv <docs-root>/plans/active/<id>-<slug> ../<repo>-<slug>/<docs-root>/plans/active/

From here the plan lives only in the worktree, next to the work it describes.

## Bootstrap

A fresh worktree carries the tracked files and nothing else. Before the first session:

1. Copy the files `.worktreeinclude` lists — gitignore syntax, repository root. It doesn't exist yet? Propose a list from the `.env*` and similar the repo actually has, and write the file after the human approves it.
2. Run the project's install command.
3. Copy, never symlink. A symlinked `node_modules` or `.env` serves two worktrees at once, and the first install in either rewrites it for both.

## Sessions

The implementing session runs inside the worktree. Tell the human to open it in `../<repo>-<slug>` and call lets-implement again; from there, resume is the ordinary one — plan.md plus that worktree's `git status`. A worktree sees the plans of its own branch: other in-flight plans stay in their branches and won't be listed here. That's isolation, not loss; once branches push, the forge shows everything.

Two cautions. Dev servers: two live worktrees default to the same port, so run one at a time or give each its own. Submodules: git calls its own support for them incomplete — `git submodule update --init` in the new worktree, or pass on worktrees for that repo.

## Record and clean up

Once the human approves the line, record the layout in AGENTS.md conventions — sibling worktrees named `<repo>-<slug>` — so later sessions expect them.

When a plan closes, lets-ship offers removal: `git worktree remove ../<repo>-<slug>` from the main checkout, after the session in the worktree has ended. The command refuses an unclean worktree, and that refusal is the safety: show what's uncommitted and let the human decide. `--force` throws the work away and is never the default. The branch survives removal; a review fix reopens the worktree with `git worktree add ../<repo>-<slug> <branch>`. A directory deleted by hand leaves a stale entry — `git worktree prune` clears it.
