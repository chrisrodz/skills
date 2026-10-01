---
name: polishing-issues
description: Make a GitHub issue self-contained so any coding agent can implement it without follow-up questions: scope, file touchpoints, acceptance criteria, validation. Use when an issue lacks scope or acceptance criteria, or before handing it to an agent. One issue at a time, not roadmaps.
---

# Polish Issue Scope

Turn one issue into an execution-ready spec for a single feature or fix. Concise, technical, no fluff.

## Workflow

1. Fetch the issue:

```bash
gh issue view <number> --repo <owner/repo> --json title,body,labels,state,comments
```

2. Scan the codebase with `rg` for related files and patterns. Note constraints: existing APIs, data models, UI patterns, tests.
3. Ask every blocking question. Confirm non-blocking assumptions with the user.
4. Draft the scope block (template below).
5. Show the exact markdown to append and wait for explicit approval before editing the issue.
6. Update the issue:

```bash
CURRENT_BODY=$(gh issue view <number> --repo <owner/repo> --json body -q .body)

gh issue edit <number> --repo <owner/repo> --body "$CURRENT_BODY

---

[scope block here]"
```

## Scope Block Template

```markdown
## Scope

**Summary**
- <1-2 sentences: the change and who it affects>

**Assumptions**
- <explicit defaults>

**Goals**
- <what must be true when done>

**Non-goals**
- <explicitly out of scope>

**Touchpoints**
- Modify: `path/to/file.ts` - <why>
- Create: `path/to/new-file.ts` - <why>

**API/data changes** (if any)
- <schema, endpoints, migrations>

**Edge cases**
- <list>

**Acceptance criteria**
- [ ] <testable outcome>

**Validation**
- Tests: `<command or file>`
- Manual: <steps>

**Tasks** (only when the work spans several commits)
1. <task> - <validation>

**Dependencies / risks**
- <libs, flags, env vars, rollout>
```

## Rules

- Prefer explicit file paths and code locations.
- With several viable approaches, list them briefly and recommend one unless the choice blocks implementation.
- Keep it scannable.
