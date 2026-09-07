# Forge recipes

## GitLab — one push creates the MR

    DESC="<description>"
    git push -u origin HEAD \
      -o merge_request.create \
      -o merge_request.target=<target> \
      -o merge_request.title="<title>" \
      -o merge_request.description="$DESC"

The MR URL lands in the push output — show it. An MR already existed on this branch → GitLab creates no duplicate but updates nothing: push options apply at creation only. Report that; edits go through the web UI or `glab` when available.

## GitHub — gh

    gh pr create \
      --base <target> \
      --head <branch> \
      --title "<title>" \
      --body "$(cat <<'EOF'
    <description>
    EOF
    )"

The PR already exists → the command fails. Offer `gh pr edit <number> --title ... --body ...` instead of retrying. `gh` missing or unauthenticated → say exactly what is missing; do not improvise around auth.

## Both

Validate the target ref exists before pushing (`git rev-parse --verify origin/<target>`). Keep title and description safely quoted; never build shell from unvalidated ref values; never force-push to fix a rejection.
