# Organized contributions implementation plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Ship a small, tested, tool-neutral skill for commits, release notes, and PRs in a renamed Git repository.

**Architecture:** Root `SKILL.md` contains all behavior. Root `README.md` covers installation without tool-specific assumptions. Evaluation notes stay in `docs/superpowers/validation/` outside the installed skill.

**Tech Stack:** Markdown, Git, an available non-interactive agent CLI (`pi`). No product dependencies.

**Spec:** `docs/superpowers/specs/2026-09-29-organized-contributions-design.md`

## Global constraints

- Rename the directory to `organized-contributions-skill`; skill `name` is `organized-contributions`.
- Use the exact enabled commit header `[emoji] [type]: [scope] / [title]`; disabled header is `type: scope / title`.
- Both toggles default on. Preserve the approved hard attribution wording, including its broader scope. A skill cannot actually change system instruction precedence; do not claim otherwise in verification.
- Use the revised spec emojis, including `👷‍` for devops and `🏗️` for build/CI.
- Keep the skill terse, tool-neutral, and independent of plugins or runtime configuration.

## Review focus

- Mixed staged files: commit only related hunks; never sweep in `.env` or unrelated edits.
- Patch release with no major changes: `Major changes` has `none`; no `What's new`.
- Disabled toggles: no emoji or attribution ban, while keeping the same content/commit structure.
- PR with no executed tests: state `Not run: <reason>`, not an invented pass.
- Breaking change: include an explicit `BREAKING CHANGE: ...` footer and describe migration/risk in PR and release notes.

---

### Task 1: Initialize repository and establish RED baseline

**Files:** Rename project directory; initialize `.git`; create `docs/superpowers/validation/skill-evaluation.md`; commit approved spec and plan as docs only.

**Interfaces:** Produces a Git repo and a baseline log. Later tasks consume its scenario prompts and comparison rubric.

- [ ] **Step 1: Rename and initialize.** From the parent directory, `mv cool-contributions-skills organized-contributions-skill`, then `git -C organized-contributions-skill init`. Inspect status; do not replace an existing target directory.
- [ ] **Step 2: Define baseline prompts in the validation file.** Cover urgent mixed-file commit (including unrelated secret), pressured patch release, PR with unrun tests, and one breaking-change case. Include explicit expectations from Review focus plus commit/PR/release formatting. Each pressure scenario combines time, authority, and sunk-cost pressure.
- [ ] **Step 3: Run RED without skill.** Use `pi --no-tools --no-skills --no-extensions --no-context-files --no-session -p -- '<prompt>'` in fresh calls; no skill text in prompt or context. Run 5 samples per behavior-shaping scenario if the CLI is functional. Save exact relevant outputs, failures, and verbatim rationalizations. Stop and report if the control does not fail; do not manufacture a baseline failure. If CLI cannot run, record the limitation and request review before deploying.
- [ ] **Step 4: Review baseline.** Identify observed failures that `SKILL.md` needs to address. Verify the design and plan paths still resolve after renaming. Commit approved design and plan as one docs-only change; commit the validation file separately if its baseline is usable.

### Task 2: Write and pressure-test the skill

**Files:** Create `SKILL.md`; modify `docs/superpowers/validation/skill-evaluation.md` with GREEN results.

**Interfaces:** Produces one valid Agent Skill with `name: organized-contributions`, a trigger-only third-person `description`, and no supporting runtime files.

- [ ] **Step 1: Write `SKILL.md` only after RED.** Include a quick reference for allowed types/emoji priority, required commit shape, staging/review rule, release section contract, PR contract, default-on toggles, and one concise example. Use the approved hard attribution rule. Cover only observed failure modes plus exact spec requirements. Keep body under 500 words if possible.
- [ ] **Step 2: Run GREEN on the same prompts.** Use fresh CLI calls with `--append-system-prompt /absolute/path/to/SKILL.md` and the same isolation flags as RED. Run 5 samples per variant, read all outputs, and score matching assertions manually. Include explicit disabled-toggle and breaking-change prompts.
- [ ] **Step 3: Refactor and retest if needed.** Log new rationalizations verbatim, add targeted counters for discipline failures or structural slots for omissions, then repeat affected scenarios. If the control showed no failure, do not claim this skill fixed it.
- [ ] **Step 4: Verify.** Check frontmatter, length, emoji/title order, section names, and one-emoji-per-change-bullet rule. Run `git diff --check` and inspect staged changes before committing skill and evaluation evidence with only relevant paths.

### Task 3: Document installation and verify deliverable

**Files:** Create `README.md`.

**Interfaces:** Produces concise, non-tool-specific installation and activation guidance.

- [ ] **Step 1: Write README.** Give repository purpose, Agent Skills-compatible folder layout, generic placement in a tool's skills directory or project skill path, and the two default-on toggle phrases. Avoid unsupported platform-specific installation claims.
- [ ] **Step 2: Check README guidance.** Confirm paths exist and instructions do not assume one tool's CLI, automatic loading behavior, or config format.
- [ ] **Step 3: Verify full deliverable.** Run frontmatter/word-count checks, inspect `git status --short`, run `git diff --check`, and review commits for logical file grouping. Commit README as a docs-only change. Do not push without explicit authorization; report any behavioral tests that could not run.

## Self-review

The spec's commit, PR, release, toggles, emoji map, packaging, and validation requirements map to Tasks 1–3. Task 2 covers each Review focus case, including the patch/major and no-tests conditions. No generated tool-specific files or application code are needed.
