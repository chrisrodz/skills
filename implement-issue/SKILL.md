---
name: implement-issue
description: Implement one scoped issue or task end to end and hand off a change with CI-equivalent checks green. Use when told to implement, build, or fix a specific issue, or when dispatched as an implementer subagent.
---

# Implement a Scoped Issue

Land one reviewable change for one scoped issue. If the issue has no scope yet, run `polishing-issues` first; a scope block in the issue is the contract.

## Workflow

1. Check the working tree. Leave pre-existing uncommitted changes alone.
2. Read the files you will touch, and the docs the repo's AGENTS.md points to for them, before editing.
3. State what is in and out of scope in a line or two, then make the smallest coherent change that follows the existing patterns. Prefer deleting or reusing over adding.
4. Run the full gate (below) and fix until green.
5. Stage explicit paths and commit per the repo's convention. Branch, push, and PR follow the repo's AGENTS.md git rules.
6. Report in the format below.

## Finding the gate

Local checks must equal what CI runs. A hand-picked subset hides failures until the PR goes red.

1. Package manager from the lockfile (`package-lock.json` npm, `yarn.lock` yarn, `pnpm-lock.yaml` pnpm). Don't swap.
2. The repo's aggregate script if it has one (`check`, `validate`, `verify`, `ci`, `precommit`).
3. Otherwise read `.github/workflows/*.yml` and run every check step, in the same form.
4. Run the formatter first when lint is format-aware.
5. A failure your change did not cause (dependency drift, flaky test, environment) is reported, not fixed in this change. Never bundle an unrelated dependency bump, and never open a PR with a red gate.

## Escalate

Report `BLOCKED` or `NEEDS_CONTEXT`, with what you tried and what you need, only when the spec contradicts the code, the task needs a design decision with several valid answers, or it is bigger than one coherent change. Otherwise keep going.

## Report

```
Status: DONE | DONE_WITH_CONCERNS | BLOCKED | NEEDS_CONTEXT
Files changed: <paths + one line each>
Tricky part: <non-obvious decisions>
Gate: <exact command> -> <result> (anything skipped and why)
Commit: <sha> <subject>  (or why not committed)
QA focus: <what a reviewer should exercise>
Concerns: <assumptions, judgment calls, anything unverified>
```

For UI or behavior changes, `qa-a-change` is the next step.
