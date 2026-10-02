# Forge recipes

The title and the description come from commit messages, the plan, and the user, so treat them as untrusted text. Load them into variables through quoted heredocs (`<<'EOF'`), which the shell doesn't expand, and pass the variables in double quotes. Never paste the text itself into a double-quoted argument: a `$(...)` or a backtick in it would run.

    TARGET=$(git symbolic-ref --short refs/remotes/origin/HEAD)   # origin/main
    TARGET=${TARGET#origin/}
    # no origin/HEAD: gh repo view --json defaultBranchRef -q .defaultBranchRef.name, else ask
    git rev-parse --verify "origin/$TARGET"
    TITLE=$(cat <<'EOF'
    <title>
    EOF
    )

Reject a branch or target name that starts with `-`.

## GitLab: one push creates the MR

    DESC=$(cat <<'EOF'
    <description, one line>
    EOF
    )
    git push -u origin HEAD \
      -o merge_request.create \
      -o "merge_request.target=$TARGET" \
      -o "merge_request.title=$TITLE" \
      -o "merge_request.description=$DESC"

Push options can't contain line breaks; git stops with "push options must not have new line characters". Keep the description on one line. The MR URL shows up in the push output. If an MR already existed on this branch, GitLab neither creates a duplicate nor updates the existing one, because push options apply only at creation. Say so, and point to the web UI or `glab mr update`.

## GitHub: gh

    gh pr create --base "$TARGET" --head "$(git branch --show-current)" \
      --title "$TITLE" --body-file - <<'EOF'
    <description>
    EOF

If a PR already exists, the command fails. Offer `gh pr edit <number> --title "$TITLE" --body-file -` instead of retrying. If `gh` is missing or not logged in, say exactly what's missing and stop; don't improvise around authentication.

Never force-push to get past a rejected push.
