---
name: implement-issue
description: Execute one scoped issue or task as a coding agent in any repo — read first, hold tight scope, run the repo's full CI-mirroring gate (not a subset), stage precise paths, and report in a fixed format. Use when told to implement/build/fix a specific issue, or when acting as an implementer subagent dispatched by an orchestrator.
---

# Implement a Scoped Issue

Goal: take one already-scoped issue/task and land a correct, reviewable change with green CI, without wandering out of scope. Optimized to be run by a cheaper model as an implementer subagent, but works the same solo.

## Use When

- Implementing a single scoped issue, feature, or fix in a repo.
- You are an implementer subagent handed a task by an orchestrator.

## Do Not Use

- The issue is not yet scoped (use `polishing-issues` first).
- Orchestrating several issues at once (that is the caller's job).
- Read-only research, or QA of a running app (use `qa-a-change`).

## Workflow

1) **Orient.** Confirm the repo, the branch you are on (assume it is already the right one unless told otherwise — do NOT switch branches or push unless the repo's AGENTS.md says you may), and the working-tree state. Note any pre-existing uncommitted changes and leave them strictly alone.

2) **Read first, edit never-before-reading.** Read the repo's `AGENTS.md` / `CLAUDE.md` (the named sections that apply), the design/QA/architecture docs they point to, and the exact files the task will touch. If the issue carries a scope block (from `polishing-issues`), that is your contract. Do not start editing until you have read every touchpoint.

3) **Restate scope and fences.** In one or two lines: what is in scope and what is explicitly out. Reuse the existing pattern in the code you are touching — extend, do not restructure. Keep logic where the repo keeps it (e.g. pure domain layer vs. UI vs. route), match local style, honor the repo's conventions (localization, no-`any`, comment discipline, etc.) as stated in its AGENTS.md.

4) **Implement the smallest coherent change.** Prefer deleting/reusing over adding. If the task turns out larger or more ambiguous than the spec implied, STOP and escalate (see below) rather than guessing.

5) **Run the full gate (see "Finding the gate").** Green before you hand off. This is the step most often shortcut — do not shortcut it.

6) **Stage precise paths only.** List the exact files. Never `git add -A` / `git add .`. Never stage unrelated pre-existing changes or generated files.

7) **Commit** using the repo's convention (usually Conventional Commits; keep the subject scoped, add whatever trailer the repo/AGENTS.md prescribes). Do not amend or force unless asked. Do not open a PR unless the repo's git rules permit it without asking — otherwise report and let the caller decide.

8) **Report** in the fixed format below.

## Finding the gate (the portable lesson)

The set of checks you run locally must equal the set CI runs. A hand-picked subset (e.g. "lint + typecheck + tests") silently skips whatever else CI enforces — a project-health/doctor check, a second test runner, a format check — and the PR goes red on a step you never ran.

1. **Detect the package manager** from the lockfile: `package-lock.json` -> npm, `yarn.lock` -> yarn, `pnpm-lock.yaml` -> pnpm. Use that one; do not swap.
2. **Prefer the repo's aggregate gate** if it defines one (seen as `check`, `validate`, `verify`, `ci`, `precommit`…). Run it.
3. **If there is no aggregate,** read `.github/workflows/*.yml` (or the repo's stated pre-handoff command in AGENTS.md) and run every check step it runs — in the same form. Assume nothing is optional.
4. **Format before committing** if the repo's lint is format-aware (biome/prettier/eslint-format), so the format check stays green.
5. **If the gate fails on something your change did not cause** — dependency/SDK version drift, a pre-existing flaky failure, an environment issue — STOP and surface it in your report. Do not bundle an unrelated dependency bump into a feature change, and never open a PR whose gate is red.

## Escalation clause

It is always OK to stop. Report `BLOCKED` or `NEEDS_CONTEXT` — with what you tried and what you need — when: the spec contradicts the actual code; the task needs a design decision with multiple valid answers; it is bigger than one coherent change; or you have been reading without progress. Bad work is worse than no work; you will not be penalized for escalating.

## Report format

```
Status: DONE | DONE_WITH_CONCERNS | BLOCKED | NEEDS_CONTEXT
Files changed: <paths + one-line each>
How the tricky part works: <the non-obvious decision(s), briefly>
Gate: <exact command run> -> <result> (note anything skipped and why)
Commit: <sha> <subject>   (or: not committed, because …)
QA focus: <what a reviewer / QA pass should specifically exercise>
Concerns: <assumptions, judgment calls, anything you could not verify>
```

Use `DONE_WITH_CONCERNS` when you finished but have doubts. Never silently ship work you are unsure about.

## Rules

- Read the touchpoints before editing. No exceptions.
- The local gate must mirror CI exactly. Discover it; don't assume `npm`.
- Stage explicit paths; never `-A`; never touch pre-existing unrelated changes.
- Match the repo's patterns, layer boundaries, and stated conventions over your own defaults.
- Escalate on contradiction or ambiguity instead of guessing.
- Keep the report factual and short; it is the caller's only window into what you did.

## Composes With

- `polishing-issues` — produces the scope block this skill executes.
- `qa-a-change` — the next step: verify the change in the running app.
- `subagent-driven-development` (if present) — this skill is what each implementer subagent follows; the orchestrator still runs spec + code-quality review.
- `create-pull-request` / `merge-pr` — PR mechanics, once the change is landed and permitted.
