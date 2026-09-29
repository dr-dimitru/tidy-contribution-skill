# Tidy contribution

An Agent Skill that makes your coding agent write clean commits, pull requests, and release notes. One `SKILL.md`, no plugin, no Git hook.

## Why use it

Agents write commits and PRs that look fine and help nobody. Typical problems:

- Commit messages like `Fix expired-session handling`, with no scope and no fixed format.
- PR descriptions that skip verification, or say "all tests passing" when nothing ran.
- Release notes that bury breaking changes in a paragraph.
- Unrelated files and secrets swept into one commit.

In my tests without the skill, all 5 samples of each of four scenarios missed the required commit header, PR verification section, or release-note structure. With the skill, they matched the format in every run.

## What it does for your workflow

- **Smaller commits.** It splits work into coherent commits, keeps tests with the change they cover, and stages only related files.
- **Scannable history.** Every header is `emoji type: scope / title`, so `git log` reads at a glance and tools can parse it.
- **Faster reviews.** A PR has a `Summary` of what changed and why, and a `Verification` section with real results or `Not run: <reason>`. Reviewers stop asking "did you test this?"
- **Breaking changes that can't be missed.** A `BREAKING CHANGE:` footer and a `⚠️` mark carry through the commit, PR, and release notes. Migration steps are required.
- **Release notes users read.** Fixed layout: `Major changes` first, then `Other Changes`. Each bullet states the result in plain words.
- **No filler.** Writing rules cut hype, vague words, and em dashes. Nothing invented: no fake tests, issue IDs, or authorship.
- **No AI credit lines** in commits, PRs, or releases, by default.

## Example

```text
⚠️ feat: api / remove legacy users endpoint

BREAKING CHANGE: GET /v1/users is removed. Use GET /v2/users.
```

## Install

```bash
npx skills add <owner>/tidy-contribution-skill
```

Flags:

- `-g` installs for your user instead of the current project.
- `-a claude-code` (or `codex`, `cursor`, and so on) targets one agent.
- `-l` lists the skills in the repo without installing.
- `-y` skips prompts.

Without `npx`, copy this folder to your tool's skills directory, or paste `SKILL.md` into your project instructions.

To apply it on every task, add this line to `CLAUDE.md` or `AGENTS.md`: `Follow the tidy-contribution-skill skill for all commits, PRs, and releases.`

## Defaults

Emoji and AI-attribution omission are on. Say "disable emojis" or "disable AI attribution preference" to turn either off for a task, or put the phrase in your repo instructions to turn it off for every task.
