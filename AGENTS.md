# AGENTS.md

Personal skills repo. Style: concise, ASCII only, no emojis.

## Layout

- One folder per skill at repo root, kebab-case, containing `SKILL.md`.
- Supporting material in the skill folder (`references/`, `scripts/`).
- `README.md` lists every skill I authored. Update it with each add/remove.
- `REFERENCES.md` catalogs other people's skills I draw from. Never vendor those here; link and give the `npx skills add` command.

## Skill rules

- `name` matches the folder name.
- `description` is trigger-focused: what it does + "Use when ...".
- Stay generic: no secrets, no machine-specific values. Per-machine overrides go in `config.local.md` (gitignored).
- Test by installing: `npx skills add . --global` from the repo root.
