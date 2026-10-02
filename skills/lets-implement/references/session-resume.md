# Session resume

Sessions end; the repository remembers. Read in this order:

1. AGENTS.md: rules, commands, conventions.
2. plan.md: status, branch, milestones, Progress (Current, Next, Blocked, Deferred scenarios), and the DEC, DEV, and Q records.
3. spec.md: the requirements and scenarios the plan serves.
4. The ADRs and RFCs the plan links.
5. `git status`, the diff, and the recent log: what actually happened in the worktree.

Then compare what the plan says with what the code shows:

- A milestone is [x] but its code is missing: untick it, add a DEV record, and tell the human.
- The code is there but the milestone is unchecked: check that it satisfies the task and its scenario, then tick it and tell the human.

A milestone marked [!] waits on a BLOCKED Q. Present that question again, and until it's answered, dispatch only the unblocked milestones.

Never resume from memory of an earlier chat. If plan.md doesn't say it happened, it didn't.
