# PR and MR descriptions

The description is written for two readers: the reviewer deciding whether to merge, and whoever digs through the history a year later wondering why the code looks like that. Fill it from the diff, the plan, and the test output — not from memory of what was intended.

## Precedence

A CONTRIBUTING.md in the project that says anything about PR or MR text wins over this file, and so does a template the project already ships (.github/PULL_REQUEST_TEMPLATE.md, .gitlab/merge_request_templates/).

## Two forms

Compressed when the change has one concern and one obvious way to check it. Full when there are several parts, a decision worth recording, or risk someone has to reason about.

### Full form

```markdown
## Summary
<What the MR does and why, in one or two sentences. Someone skimming the history later should understand the change from this alone.>

## Why
<The problem and where it came from: ticket, plan, design doc, bug report. Links support the story and don't carry it — they rot, and not every future reader can open them.>

## Changes
<Grouped by intent — added, changed, removed. Plain language, no file lists; the diff already is one.>

## How
<Delete unless the diff hides a decision: the approach taken, the alternative rejected and why, the constraint that forced this shape.>

## Verification
<How it was checked, so a reviewer can repeat it: the commands with the output that mattered, manual steps one action at a time, the CI run to point at.>

## Screenshots
<Delete unless the UI changed. Before and after.>

## Risk and rollback
<Delete unless this touches a service, data, or an interface others depend on: what can break and for whom, how to roll back, deploy or migration order, anything sensitive the diff now handles.>

## Reviewer notes
<Delete unless it earns its place: where to start, the order to read the commits in, what to look at hardest.>

## Out of scope
<Delete unless something was knowingly left: the gap, the follow-up, the ticket it went to.>
```

### Compressed form

```markdown
## Summary
<What and why, one to three sentences.>

## Verification
<The command or step that shows it works, with the output that matters.>
```

## Filling it in

- Every fact comes from the diff, the plan, or real output. What you don't know is a `TODO: <what's missing>` left in place, never a guess.
- Delete the sections that don't apply; an empty heading is noise.
- Write Changes by walking the diff — it doubles as a self-review, and it's where a forgotten file surfaces.
- Verification a reviewer can't repeat isn't verification. Name the command, the result, the CI run.
