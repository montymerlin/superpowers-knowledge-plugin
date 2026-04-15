# CLAUDE.md — Superpowers MM Plugin

This is the **Superpowers for Knowledge Work** plugin — a deliberate fork of [Superpowers](https://github.com/obra/superpowers) by Jesse Vincent, adapted for creative, strategic, and business workflows by Rollo Bryant.

## What This Repo Is

A Claude Code plugin that ships structured workflow discipline for non-code knowledge work. The plugin enforces brainstorm → plan → execute → review → verify gates that prevent ad-hoc execution and ensure evidence-based completion.

## Structure

```
.claude-plugin/
  plugin.json          — plugin metadata (name, version, author)
skills/
  <skill-name>/
    SKILL.md           — the skill document loaded by the Skill tool
UPSTREAM.md            — sync history and methodology mapping vs. upstream
ROADMAP.md             — future directions and improvement ideas
CHANGELOG.md           — narrative change history
DECISIONS.md           — architectural decision log
```

## Key Conventions

- **Skills live in `skills/<name>/SKILL.md`** — each skill is a single markdown file. No subdirectories within skill folders unless adding `references/` for supporting material.
- **Plugin metadata is in `.claude-plugin/plugin.json`** — update `version` on every release.
- **Bump version on release** — follows semantic versioning. Patch for skill tweaks, minor for new skills, major for methodology overhauls.
- **UPSTREAM.md is the source of truth** for what we've adopted and why. Update the Sync Status table after every upstream review.

## Skill Authoring

When creating or editing a skill:

1. Follow the `writing-skills` skill methodology (hypothesis-driven, test before writing)
2. Every skill needs: frontmatter (`name`, `description`), an Iron Law, When to Use, When NOT to Use, and the process
3. Descriptions must trigger correctly — they're used by the harness to match skill invocations
4. After editing, re-package: run the `.plugin` build step and update the version

## Relationship to Upstream

This is a **deliberate fork**, not a mirror. Upstream targets software development; this plugin targets knowledge work. See UPSTREAM.md for the full skill mapping and review process.

**Review upstream** when a new Superpowers version is released — diff the shared skills, adopt methodology improvements, skip code-specific content.

## Claude Code Responsibilities

- Editing or reviewing skills → follow the `writing-skills` methodology
- Adding a new skill → check UPSTREAM.md first (does an upstream equivalent exist to adapt?)
- Releasing a version → bump `plugin.json`, update UPSTREAM.md Sync Status, add CHANGELOG entry, commit and push
- Upstream sync → follow the "How to Review" steps in UPSTREAM.md
