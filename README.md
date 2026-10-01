# Skills

My [agent skills](https://code.claude.com/docs/en/skills). Each skill is a folder with a `SKILL.md` (name + description frontmatter, then instructions) that an agent loads on demand when the task matches.

Skills I use but did not write are catalogued in [REFERENCES.md](REFERENCES.md).

## Available skills

### [daily-note](daily-note/SKILL.md)

Transitions an Obsidian daily note from one day to the next. Closes out the outgoing day (Done, meeting recaps, end-of-day compound) and opens the incoming one (carry-over, meeting prep, prioritized plan) by pulling Slack, GitHub, task-tracker, calendar, and meeting-notes activity.

Use it when:

- Running a start-of-day or end-of-day routine
- Planning the day, wrapping up the day, or rolling notes forward

> Generic by design: all environment values are `{{TOKENS}}` in `references/config.md`. Per-machine overrides go in `references/config.local.md` (gitignored).

### [implement-issue](implement-issue/SKILL.md)

Executes one scoped issue or task as a coding agent in any repo. Reads first, holds tight scope, runs the repo's full CI-mirroring gate (not a subset), stages precise paths, and reports in a fixed format.

Use it when:

- Told to implement, build, or fix a specific issue
- Acting as an implementer subagent dispatched by an orchestrator

### [polishing-issues](polishing-issues/SKILL.md)

Makes a GitHub issue self-contained for a single feature or fix so any coding agent can execute it without back-and-forth. Focuses on scope, file touchpoints, acceptance criteria, and validation.

Use it when:

- An issue is vague and needs to be agent-ready before work starts

### [qa-a-change](qa-a-change/SKILL.md)

QAs a change end-to-end by driving the real running app: web via agent-browser, native/mobile via agent-device. Checks a behavior checklist, screenshots each state, flags the safety-critical path, never fakes a PASS, and reports PASS/FAIL/NOT-COVERED with a verdict.

Use it when:

- Before merging a UI or behavior change
- Dispatched as a QA subagent

> Pairs with the `agent-browser` and `agent-device` skills (see [REFERENCES.md](REFERENCES.md)).

## Installation

Use `npx skills` to install to most coding agents:

```bash
# everything
npx skills add chrisrodz/skills --global

# one skill
npx skills add chrisrodz/skills@qa-a-change --global
```

Claude Code invokes a skill automatically when a task matches its description. You can also call one explicitly, e.g. `/qa-a-change`.

## Adding a new skill

1. Create a kebab-case folder named after the skill.
2. Add a `SKILL.md` with `name` and `description` frontmatter. The description decides when the skill applies, so make it trigger-focused ("Use when...").
3. Keep instructions concise and actionable; link to reference files in the folder when they get long.
4. Add an entry to the list above.
