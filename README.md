# Organized contributions

Tool-neutral Agent Skill for focused commits, concise PRs, and plain-language release notes. Rules live in [`SKILL.md`](SKILL.md).

## Install

```bash
npx skills add <owner>/organized-contributions-skill
```

Flags:

- `-g` installs for your user instead of the current project.
- `-a claude-code` (or `codex`, `cursor`, and so on) targets one agent.
- `-l` lists the skills in the repo without installing.
- `-y` skips prompts.

Without `npx`, copy this folder to your tool's skills directory, or paste `SKILL.md` into your project instructions.

## Defaults

Emoji and AI-attribution omission are on. Say "disable emojis" or "disable AI attribution preference" to turn either off for a task. This skill does not require a plugin or Git hook.
