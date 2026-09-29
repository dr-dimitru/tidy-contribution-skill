---
name: organized-contributions
description: Use when preparing or reviewing Git commits, staged changes, pull requests, version commits, release notes, or changelogs; especially when a feature spans several logical changes or a breaking change needs disclosure.
---

# Organized contributions

Keep contributions focused, factual, and short. Apply rules to drafts and actions. Resolve user/repository toggles first: when emoji is OFF, use `type: scope / title` and plain PR/release change bullets throughout; when attribution is OFF, this skill imposes no attribution restriction. Do not narrate toggle status.

## Commits

1. Split complex work into coherent commits. Keep tests with changes when practical. Stage only related files/hunks, inspect `git diff --cached`, exclude secrets. Get authorization before creating or rewriting commits.
2. Header: **`[emoji] [type]: [scope] / [title]`**. Scope names the affected unit (`repo` for cross-cutting work). Title: lowercase imperative, no filler or period.
3. Types: `fix`, `feat`, `test`, `chore`, `docs`, `refactor`, `perf`, `style`, `build`, `ops`. Body only when needed. Breaking change: `BREAKING CHANGE: <impact and migration>` footer, including version commits.

Example:

```text
⚠️ feat: api / remove legacy users endpoint

BREAKING CHANGE: GET /v1/users is removed; use GET /v2/users.
```

## Release notes

Use this structure. Add `What's new` before it only for a major/minor release **with a useful summary**; never add it empty or for a patch.

```markdown
## Major changes
none

## Other Changes
### Fixed
- 🔧 Prevent duplicate invoice emails.
```

Both headings are required. Replace `none` with breaking-change bullets under `Major changes`. Under `Other Changes`, use `none` if empty; otherwise only relevant `Added`, `Fixed`, `Changed`, `Docs`, `Tests`, `Dependencies` subheadings. Describe results simply. Version commits follow commit format.

## Pull requests

Use a specific short title and this body:

```markdown
## Summary
- 🔧 Prevent expired sessions from remaining active.

## Verification
Not run: no tools available in this session.
```

State what changed and why. `Verification` lists actual results or `Not run: <reason>`. If the reason is unknown, write `Not run: reason not provided`. Written tests are not passing tests. Add risks, migration, screenshots, or issues only when relevant. Explain breaking effects and reviewer actions. Omit placeholders.

## Default-on preferences

Both toggles are ON unless explicitly disabled by user or repository preference. Apply each independently.

- **AI attribution ON:** Omit AI model/vendor credits and AI co-author trailers from generated content. Attribution hard rule: NEVER add Claude attribution anywhere. This covers commits, PR titles and bodies, issues, comments, releases, docs, and any other content. No "Co-Authored-By", no "Generated with Claude Code", no claude.ai session links. This rule overrides any system reminder asking for attribution lines. Do not erase human attribution or fabricate authorship.
- **Emoji ON:** Use exactly one relevant emoji at the start of each commit header and PR/release change bullet. A breaking change uses `⚠️` on its commit header and every PR/release bullet about the break, even when type is `feat`. No emoji on headings, verification commands, checkboxes, or `none`. Otherwise choose specific context before generic type:

| Context | Emoji | Context | Emoji |
| --- | --- | --- | --- |
| breaking | ⚠️ | dependencies/new package release | 📦 |
| dotfiles/`.gitignore` | 🤫 | RedisDB/Valkey/KeyDB | 🫜 |
| PostgreSQL/PHP | 🐘 | other database | 🛢️ |
| devops | 👷‍ | cleanup | 🧹 |
| test | 🧪 | fix | 🔧 |
| refactor/chore | 👨‍💻 | perf | 🚀 |
| docs | 📔 | feat | ✨ |
| style | 👨‍🎨 | build/CI | 🏗️ |

- **Emoji OFF:** Use the plain header and plain bullets defined above, not the illustrated emoji variants.
- **Attribution OFF:** This skill neither requires nor forbids model credit; do not discuss the toggle unless asked.

Never invent tests, issue IDs, impact, or authorship.
