# Setup Guide

Structured workflow discipline for creative, business, and strategic knowledge work.

---

## Quick Install (for AI agents)

If you're an AI agent installing this plugin, **detect the host first**, then pick the matching path. Only ask the user the questions explicitly listed below.

```
1. Detect host:
   ├── Cowork (Claude Desktop, sandboxed)
   │     → Path A: Cowork upload (no questions needed)
   │
   ├── Claude Code CLI (terminal, has `claude` command)
   │     → Path B: claude plugins install
   │     → ASK USER: "Install globally (every project) or locally (this project)?"
   │       • global → `claude plugins install github.com/montymerlin/superpowers-knowledge-plugin`
   │       • local  → symlink `ln -s <path> ./.claude/plugins/superpowers-knowledge`
   │
   ├── Codex (terminal, has `codex` command or $CODEX_HOME set)
   │     → Path C: bash scripts/install_codex_skills.sh --from-github
   │
   ├── Cursor / VS Code
   │     → Path D: Raw skills only (no plugin manifest support)
   │       Copy `skills/*/SKILL.md` files into the host's skill dir.
   │
   └── Unknown / custom Agent SDK host
         → Path D: Raw skills — same as Cursor/VS Code path above.
```

**Host detection signals:**
- `$CLAUDE_COWORK == "1"` or `mount | grep virtiofs` matches → Cowork
- `command -v claude` succeeds and not Cowork → Claude Code CLI
- `command -v codex` succeeds or `$CODEX_HOME` is set → Codex
- Otherwise → ask the user which environment they're in.

---

## Compatibility Matrix

| Host | Status | Notes |
|------|--------|-------|
| **Cowork** | ✓ | One-click plugin upload, skills in `/` menu |
| **Claude Code CLI** | ✓ | `claude plugins install github.com/montymerlin/superpowers-knowledge-plugin` |
| **Codex** | ✓ | `bash scripts/install_codex_skills.sh --from-github` |
| **Cursor / VS Code** | partial | No plugin manifest support; copy `skills/*/SKILL.md` into the host's skill folder |
| **Agent SDK** | ✓ | Standard plugin loader |
| **Anthropic API direct** | partial | Manual skill instruction wiring |

---

## Cowork (Claude Desktop)

Cowork provides the smoothest experience: one-click plugin install and skill discovery via the `/` menu.

You need a `.plugin` zip to upload. Get one of these three ways:

**Option 1 — pre-built release (preferred when available):**
Download `superpowers-knowledge-<version>.plugin` from the GitHub Releases page of `montymerlin/superpowers-knowledge-plugin`.

**Option 2 — built locally from this repo:**

```bash
git clone https://github.com/montymerlin/superpowers-knowledge-plugin.git
cd superpowers-knowledge-plugin
zip -r /tmp/superpowers-knowledge-0.5.0.plugin . \
  -x "*.DS_Store" "*/__pycache__/*" "*.pyc" ".git/*" "node_modules/*" "*.log" "_dist/*"
```

The output `/tmp/superpowers-knowledge-0.5.0.plugin` is your upload artifact.

**Option 3 — built by the workspace `cowork-plugin-packager` skill** (montymerlinHQ collaborators only):
The packaged file lives at `ops/plugins/_dist/superpowers-knowledge-0.5.0.plugin` after running the skill.

Then upload:

1. Open Claude Desktop → **Cowork** → **Plugins** in the sidebar.
2. Click **+ Add plugin** → **Upload a file** → select the `.plugin`.
3. Confirm install. Skills appear under `/brainstorming`, `/writing-plans`, etc.

**Pre-upload verification (recommended):**

```bash
# Confirm the manifest is at the zip root
unzip -l /tmp/superpowers-knowledge-0.5.0.plugin | head -20

# Confirm size is under 50 MB (this plugin packages to ~62 KB)
du -h /tmp/superpowers-knowledge-0.5.0.plugin
```

**What gets installed:** Ten skills for knowledge-work methodology (brainstorming, writing-plans, executing-plans, verification-before-completion, using-superpowers, systematic-problem-solving, two-stage-review, feedback-reception, parallel-work, writing-skills).

**Known quirks:**
- File size limit: 50 MB. This plugin is well under the limit.
- Some Claude Desktop builds reject `.plugin` extension at upload despite docs accepting it. Workaround: rename to `.zip` (contents identical). See [anthropics/claude-code#28337](https://github.com/anthropics/claude-code/issues/28337) and [#40414](https://github.com/anthropics/claude-code/issues/40414).
- Ensure `.claude-plugin/plugin.json` is at the top level of the `.plugin` zip (not nested inside an extra parent directory). The `zip` command above runs from inside the plugin dir specifically to avoid this.

---

## Claude Code CLI

Two install scopes — **ask the user which one fits**:

- **Global** (every project on this machine): `claude plugins install github.com/montymerlin/superpowers-knowledge-plugin`
- **Local** (this project only, lives in `./.claude/plugins/`): symlink the cloned repo

**Global install:**

```bash
claude plugins install github.com/montymerlin/superpowers-knowledge-plugin
```

**Local install** (project-scoped):

```bash
git clone https://github.com/montymerlin/superpowers-knowledge-plugin.git ~/src/superpowers-knowledge-plugin
mkdir -p ./.claude/plugins
ln -s ~/src/superpowers-knowledge-plugin ./.claude/plugins/superpowers-knowledge
```

Skills load automatically once installed. Invoke by name or natural language in the chat.

---

## Codex (OpenAI)

```bash
bash scripts/install_codex_skills.sh --from-github
```

The script writes skill stubs to `~/.codex/skills/` that source from a vendor clone of the repo.

---

## Cursor / VS Code

This is a **markdown-skills-only plugin with no MCP**. It works in any host that loads skills from `.claude-plugin/` metadata or raw `skills/` directories. In Cursor and VS Code, copy individual skill markdown files into your local skills folder to use them.

Alternatively, extract the `.plugin` file (it's a ZIP) and copy the `skills/` directory to your project.

---

## Agent SDK & Anthropic API Direct

For Agent SDK custom hosts: load skills from the `skills/` directory using your host's standard skill loader.

For Anthropic API direct: copy SKILL.md instruction text into system prompts and wire tools manually using tool definitions. See `AGENTS.md` for the canonical skill structure.

---

## Implementation Notes

**No runtime dependencies:** This plugin is pure Markdown. All 10 skills work offline. No Python, Node, or external tools required. Safe for sandboxes.

**Upstream relationship:** This is a deliberate fork of [Jesse Vincent's Superpowers](https://github.com/obra/superpowers), adapted for non-code knowledge work. The core methodology (Iron Laws, verification gates) is shared; the domain-specific skills differ. See [UPSTREAM.md](UPSTREAM.md) for full lineage and coexistence strategy.

**Coexistence:** Install alongside official Superpowers. Skills are domain-scoped so agents route by context: code tasks → official skills, knowledge tasks → this plugin's skills.
