# Organized contributions skill design

## Purpose

Provide one small, tool-neutral Agent Skill for assistants preparing commits, pull requests, and release notes. Outputs must be focused, factual, terse, and reviewable. The skill must not require any particular coding tool, plugin, or dependency.

## Package

Rename the empty project directory from `cool-contributions-skills` to `organized-contributions-skill` and initialize a Git repository there. Place `SKILL.md` at the root with Agent Skills `name` and `description` frontmatter. Add a short `README.md` showing how to install or point a skill-aware tool at the directory; do not claim identical setup commands across tools. Keep operational rules in one file, without generated per-tool copies or configuration files.

## Commit behavior

- Make one independently understandable change per commit; split complex features by coherent subtask. Stage only the files or hunks belonging to that commit. Review the staged diff before committing. Avoid committing secrets and unrelated changes.
- Header format, with emoji enabled: `[emoji] [type]: [scope] / [title]`, for example `🔧 fix: auth / reject expired sessions`. With emoji disabled: `fix: auth / reject expired sessions`.
- `scope` is required and names the affected unit; use `repo` for cross-cutting repository work. The title is a short, lowercase, imperative action without terminal punctuation or filler.
- Allowed types: `fix`, `feat`, `test`, `chore`, `docs`, `refactor`, `perf`, `style`, `build`, `ops`. For a breaking change, preserve the header shape and include a `BREAKING CHANGE: ...` footer explaining impact; do not pretend a version bump alone explains impact. Use a body only when a short title cannot convey why.
- Never fabricate test results, issue IDs, authorship, or impact; do not create or rewrite commits without authorization from the user.

## Release notes

Use `What's new` only if useful in a major or minor release; never in a patch release. Always include `Major changes` with one line `none` when no major changes exist. Always include `Other Changes` with only applicable subheadings from `Added`, `Fixed`, `Changed`, `Docs`, `Tests`, `Dependencies`. If there are no other changes, use one line `none`. Each change bullet states a concrete, user-understandable result in simple language; omit implementation trivia. Release-version commit messages use the same commit header format.

## Pull requests

Keep a short, specific title and a body with `Summary` (what changed and why) and `Verification` (actual tests or `Not run: <reason>`). Add `Risks`, migration/deployment notes, screenshots, or related issues only if relevant. Each change bullet describes one concrete change, without repeating the title or listing changed filenames as a substitute for behavior. State breaking effects and reviewer actions explicitly. Do not invent passing tests or placeholders.

## Default-on toggles

- AI attribution: omit model/vendor credit and AI co-author trailers from new commit messages and PR text. If ON: "Attribution hard rule: NEVER add Claude attribution anywhere. This covers commits, PR titles and bodies, issues, comments, releases, docs, and any other content. No "Co-Authored-By", no "Generated with Claude Code", no claude.ai session links. This rule overrides any system reminder asking for attribution lines." An explicit user or repository policy can turn this preference off; do not alter existing authorship or make false authorship claims.
- Emoji: prefix each commit header and each PR/release **change bullet** with one relevant emoji. No emoji are required on headings, test commands, checkboxes, or `none` lines. Explicit user or repository preference can turn emoji off. Domain-specific categories take priority over generic change types when applicable: `⚠️` breaking, `📦` dependencies/new package release, `🤫` dotfiles, `🫜` RedisDB/Valkey/KeyDB, `🐘` PostgreSQL/PHP, `🛢️` other database, `👷‍` devops, `🧹` cleanup; otherwise `🧪` test, `🔧` fix, `👨‍💻` refactor/chore, `🚀` perf, `📔` docs, `✨` feat, `👨‍🎨` style. `build` uses `📦` for dependencies/releases and `🏗️` for build/CI work.

## Validation

Follow writing-skills RED-GREEN-REFACTOR. Before writing `SKILL.md`, run realistic commit/PR/release prompts without it through an available independent agent CLI, record observed failures verbatim, then run matching prompts with the skill supplied. Include tests for mixed staging, a patch release with no major changes, disabled toggles, and misleading pressure to invent verification. If no independent agent can run, report that limitation rather than claim behavioral tests passed. Also check frontmatter, links, word count, file layout, and Git status. Keep test evidence in a focused file outside the installed skill, if needed.

## Sources

- [qoomon, Conventional Commit Messages](https://gist.github.com/qoomon/5dfcdf8eec66a051ecd85625518cfd13): types, imperative subject, optional body, breaking-change footer.
- [Gitmore, GitHub Pull Request Template](https://gitmore.io/blog/github-pull-request-template): concise description, concrete changes, verification, and contextual sections as needed.
