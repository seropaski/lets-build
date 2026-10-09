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

## GitLab: glab carries the full description, push options don't

The template description has line breaks; push options reject them — git stops with "push options must not have new line characters". When glab is installed, push plain and let it create the MR (the source branch defaults to the current one):

    DESC=$(cat <<'EOF'
    <description, multi-line>
    EOF
    )
    git push -u origin HEAD
    glab mr create --target-branch "$TARGET" --title "$TITLE" --description "$DESC"

Without glab, fall back to push options, with the Summary section alone as the description — it must stay on one line — and tell the human the rest of the template has to be pasted in the web UI:

    DESC=$(cat <<'EOF'
    <summary line only>
    EOF
    )
    git push -u origin HEAD \
      -o merge_request.create \
      -o "merge_request.target=$TARGET" \
      -o "merge_request.title=$TITLE" \
      -o "merge_request.description=$DESC"

The MR URL shows up in the push output. If an MR already existed on this branch, GitLab neither creates a duplicate nor updates the existing one: push options apply only at creation and `glab mr create` fails. Say so, and point to the web UI or `glab mr update`.

## GitHub: gh

    gh pr create --base "$TARGET" --head "$(git branch --show-current)" \
      --title "$TITLE" --body-file - <<'EOF'
    <description>
    EOF

If a PR already exists, the command fails. Offer `gh pr edit <number> --title "$TITLE" --body-file -` instead of retrying. If `gh` is missing or not logged in, say exactly what's missing and stop; don't improvise around authentication.

Never force-push to get past a rejected push.
