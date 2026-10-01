---
name: qa-a-change
description: QA a change end-to-end by driving the real running app — web via agent-browser, native/mobile via agent-device — against a behavior checklist, screenshotting each state, flagging the safety-critical path, never faking a PASS, and reporting PASS/FAIL/NOT-COVERED with a verdict. Use before merging a UI or behavior change, or when dispatched as a QA subagent.
---

# QA a Change in the Running App

Goal: prove a change actually works by exercising it in the real app and observing behavior — not by re-reading the diff. Produce screenshots a reviewer can trust and a clear ship / no-ship verdict.

## Use When

- A UI or user-facing behavior change needs verification before merge.
- You are a QA subagent handed a specific change to verify.
- A PR needs embedded visual evidence.

## Do Not Use

- Pure logic/domain changes with no runtime surface (a unit test is the right tool).
- Implementing or fixing the change (that is `implement-issue`; here you observe and report, and hand defects back).

## Workflow

1) **Read the repo's QA doc first.** Find and follow it (`docs/qa.md`, AGENTS.md "QA" section, or similar): how to run the app, the selector convention (many repos require `testID`/stable ids, not visible text), reset/seed tools, dev shortcuts, and where screenshots are hosted. Reuse any prior-pass knowledge the repo or thread records (e.g. "cold-relaunch after a code change so hot-reload state doesn't hide new UI").

2) **Pick the driver by platform.**
   - Web app -> the `agent-browser` skill (phone viewport for mobile-web).
   - Native / mobile (iOS, Android, Expo) -> the `agent-device` skill.
   Load that skill for the mechanics; this skill governs the *process*.

3) **Restate what shipped** in behavioral terms — the flows and states you must exercise, not the code.

4) **Build a checklist**, one row per observable behavior. Explicitly mark the **safety-critical or destructive path** ("be rigorous here") — the one where a wrong result actually harms a user. Cover: happy path, the edge/skip paths, empty states, dark mode, and each locale the repo ships (longer translations are where layouts break).

5) **Drive it and screenshot each key state.** The screenshot is ground truth; when the accessibility snapshot looks stale or sparse, trust the screenshot. Save screenshots to a scratch dir the repo ignores (e.g. `artifacts/qa-<id>/`); do not commit them to the feature branch.

6) **Never fake a PASS.** If you cannot synthesize a real interaction (a precise long-press, a hardware event, a network condition), say so plainly and fall back to verifying that path by reading the code — and label it as code-verified, not observed. A silent "PASS" you did not actually witness is the one failure mode that destroys the value of QA.

7) **Be picky.** Spacing, contrast in both themes, text truncation, long-locale fit, tap-target size, broken/placeholder images. A working feature that looks broken is a defect.

8) **On PASS, publish evidence** per the repo's convention (e.g. an orphan `pr-assets`-style branch, an artifact upload, or attaching to the PR) — pushing only that asset location, never the feature branch. Provide ready-to-embed snippets. **On a ship-blocking defect, do NOT publish** — report the defect with a precise repro (and file/line if you can find it) and hand it back.

9) **Report** in the fixed format below.

## Report format

```
Verdict: PASS | PASS WITH NITS | FAIL (blocking)
Driver: agent-browser | agent-device  (platform, device/viewport)
Checklist:
  1. <behavior> — PASS | FAIL | NOT-COVERED — <one line, incl. how verified>
  ...
  <safety-critical item flagged, with how rigorously it was checked>
Defects: <blocking first; repro steps; file/line if known; note if pre-existing/out-of-scope>
Screenshots: <files, and the published/embeddable snippets if PASS>
Not covered: <what you could not exercise and why>
```

## Rules

- Follow the repo's QA doc and selector convention; do not invent your own.
- Observe behavior in the running app; the diff is not evidence.
- Screenshot is ground truth over stale snapshots.
- Never report a PASS you did not witness — code-verify and label instead.
- Flag the safety-critical path and check it hardest.
- Distinguish defects this change introduced from pre-existing ones (check with `git blame`/`git show`); report both, scope them honestly.
- Only publish evidence on PASS; only the asset location, never the feature branch.

## Composes With

- `agent-device` / `agent-browser` — the drivers this skill orchestrates.
- `implement-issue` — hand blocking defects back to it; re-QA after the fix.
- The repo's `docs/qa.md` / AGENTS.md QA section — the source of truth for run + screenshot conventions.
