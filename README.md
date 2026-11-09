# Superpowers for Knowledge Work — retired

> **This plugin was retired on 2026-11-09 and is no longer maintained.**
> Use Jesse Vincent's [Superpowers](https://github.com/obra/superpowers) instead. It now covers knowledge work as well as software.

## Why it was retired

This repo was a fork of [Superpowers](https://github.com/obra/superpowers), adapted in April 2026 (from upstream v5.0.7) for creative, strategic and business work rather than code. It existed because upstream was written for software development.

That reason has gone. Upstream's brainstorming skill now applies to "planning anything new, in software or out of it (a talk, a business, a renovation)", and it has been rebuilt and tuned twice since this fork was taken (v7.0.0 to v7.0.2). The fork stopped receiving upstream improvements in April, and installing both meant two near-identical sets of skills competing for the same tasks.

The reasoning is recorded in [DECISIONS.md](DECISIONS.md), Decision 007.

## What to use instead

Install Superpowers from its author's marketplace:

```bash
claude plugin marketplace add obra/superpowers-marketplace
claude plugin install superpowers@superpowers-marketplace
```

For other hosts (Codex, Cursor, OpenCode and more), follow the [Superpowers README](https://github.com/obra/superpowers#readme).

If you have this plugin installed, uninstall it:

```bash
claude plugin uninstall superpowers-knowledge@superpowers-knowledge
claude plugin marketplace remove superpowers-knowledge
```

In Cowork, remove it under Claude Desktop → Plugins. For Codex, delete the `superpowers-knowledge-*` entries from `~/.codex/skills/`.

## What was here

Ten markdown skills: `using-superpowers`, `brainstorming`, `writing-plans`, `executing-plans`, `verification-before-completion`, `parallel-work` and `writing-skills` (adaptations of upstream), plus three originals, `systematic-problem-solving`, `two-stage-review` and `feedback-reception` (evaluating client and stakeholder feedback before acting on it). The files stay in this repo as a record; [UPSTREAM.md](UPSTREAM.md) maps each to its upstream counterpart.

## License

MIT
