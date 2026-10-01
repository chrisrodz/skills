---
name: qa-a-change
description: QA a UI or behavior change by driving the real running app (agent-browser for web, agent-device for native/mobile) against a behavior checklist, with screenshots and a ship/no-ship verdict. Use before merging a user-facing change, or when dispatched as a QA subagent.
---

# QA a Change in the Running App

Prove the change works by exercising it in the real app, not by re-reading the diff. Skip pure logic changes with no runtime surface; a unit test fits those.

## Workflow

1. Read the repo's QA doc first (`docs/qa.md` or the AGENTS.md QA section): how to run the app, the selector convention, reset/seed tools, where screenshots are hosted, and prior-pass lessons it records.
2. Pick the driver: web uses the `agent-browser` skill (phone viewport for mobile web); native and mobile use `agent-device`. Load it for mechanics.
3. Restate what shipped as behavior, then write a checklist with one row per observable behavior: happy path, edge and skip paths, empty states, and each theme and locale the repo ships. Mark the safety-critical or destructive path and check it hardest.
4. Drive the app and screenshot each key state. The screenshot is ground truth over a stale accessibility snapshot. Save to a repo-ignored scratch dir (for example `artifacts/qa-<id>/`), never to the feature branch.
5. Report a PASS only for what you witnessed. If an interaction can't be synthesized, say so, verify by reading the code, and label it code-verified.
6. Be picky: spacing, contrast, truncation, tap targets, broken images. A working feature that looks broken is a defect.
7. Separate defects this change introduced from pre-existing ones (`git blame`) and report both.
8. On PASS, publish evidence per the repo's convention, pushing only the asset location (never the feature branch), with ready-to-embed snippets. On a blocking defect, publish nothing; report a precise repro (file and line if known) and hand it back to `implement-issue`.

## Report

```
Verdict: PASS | PASS WITH NITS | FAIL (blocking)
Driver: agent-browser | agent-device (platform, device/viewport)
Checklist:
  1. <behavior> - PASS | FAIL | NOT-COVERED - <how verified>
Defects: <blocking first; repro; file/line; pre-existing or introduced>
Screenshots: <files, plus embeddable snippets on PASS>
Not covered: <what you could not exercise and why>
```
