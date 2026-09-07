# Session resume

Sessions die; the repository is the memory. Recovery order:

1. AGENTS.md — rules, commands, conventions.
2. plan.md — status, milestones, Progress (Current / Next / Blocked), DEC / DEV / Q records.
3. spec.md — the requirements and scenarios the plan serves.
4. ADRs and RFCs the plan links.
5. git status, diff, recent log — what actually happened to the worktree.

Then reconcile: the plan says, the code shows.

- milestone [x] but the code is absent → untick, DEV record, tell the human;
- code present but the milestone is unchecked → verify it satisfies the task and its scenario, then tick;
- both directions get a one-line note to the human.

Status IN_PROGRESS with a milestone [!] (its Q BLOCKED) → re-present that question; until it is answered, dispatch only unblocked milestones. Status BLOCKED → nothing can move: re-present the questions; a human answer resolves the Q, returns the status to IN_PROGRESS, and work resumes. Status IN_PROGRESS without blockers → continue the loop at the first unchecked milestone. Status READY → implementation never started; begin at M1. Status IN_REVIEW belongs to sdf-review; sdf-implement does not resume it.

A session never resumes "from memory" of a previous chat. If the plan does not state it, it did not happen.
