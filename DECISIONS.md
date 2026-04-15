# Decisions

Architectural decisions for the Superpowers MM Plugin. Log significant choices here *before* implementing, using the format below.

---

## Decision 001 — Deliberate fork over mirror (2026-04-03)

**Context:** Superpowers upstream targets software development workflows. The montymerlinHQ use case is primarily creative, strategic, and business knowledge work — proposals, campaigns, research, strategy documents — where code-specific skills (TDD, git workflows, debugging) don't apply.

**Decision:** Maintain a deliberate fork, selectively adopting upstream methodology improvements while replacing code-specific content with knowledge-work equivalents.

**Consequences:** We stay current on methodology (Iron Laws, verification patterns, rationalization prevention) while keeping domain-specific content relevant. The cost is ongoing maintenance overhead from tracking upstream.

**Alternatives Considered:**
- *Mirror upstream exactly* — rejected. Too many code-specific skills that would confuse or not trigger in a knowledge-work context.
- *Wrapper plugin that extends upstream* — rejected. Skill precedence rules make this complex; cleaner to own the full skill set.

---

## Decision 002 — Adopted agentic scaffold (2026-04-15)

**Context:** The plugin repo lacked CLAUDE.md, CHANGELOG.md, and DECISIONS.md, making it harder for Claude Code to understand conventions and for the history to be legible.

**Decision:** Add the standard agentic scaffold (CLAUDE.md, CHANGELOG.md, DECISIONS.md) alongside the existing README.md and ROADMAP.md.

**Consequences:** The repo is now a first-class agentic workspace. Claude Code has explicit instructions for skill authoring, versioning, and upstream sync.

**Alternatives Considered:**
- *Leave as-is* — rejected. Without CLAUDE.md, conventions have to be re-explained each session.
