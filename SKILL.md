---
name: workspace-health
description: Audits an OpenClaw workspace for configuration health, signal quality, and security issues. Use when asked to run a health check, audit the workspace, review agent config quality, or check if AGENTS.md, SOUL.md, memory files, or skills are in good shape. Checks for: bloated bootstrap files, stale memory, skill description quality, prompt injection risks in skills, critical rules coverage, and context hygiene issues. OpenClaw equivalent of claude-health.
---

# Workspace Health

Audit an OpenClaw workspace across five layers. Detect what to fix and in what order.

Read `references/checks.md` for the full list of checks per layer.

## Layers

1. **Bootstrap files** — AGENTS.md, SOUL.md, TOOLS.md, USER.md, IDENTITY.md
2. **Memory** — MEMORY.md index, memory/*.md files, open-items.md
3. **Skills** — SKILL.md quality, descriptions, security
4. **Cron jobs** — prompt quality, timeouts, silent failure patterns
5. **Process discipline** — open items, daily log hygiene, session close habits

## How to Run

1. Detect workspace root (default: `/Users/leos/.openclaw/workspace`)
2. Read all bootstrap files
3. Read all memory/*.md files and MEMORY.md
4. Read all skills/*/SKILL.md files
5. List cron jobs via cron tool
6. Run all checks from `references/checks.md`
7. Output prioritised report

## Output Format

Group findings into three levels:

**Critical - Fix now**
- Security issues in skills (prompt injection, hardcoded secrets, destructive commands)
- Open items that are blocking or overdue
- Cron jobs with silent failure patterns
- Bootstrap files with dangerous or conflicting instructions

**Structural - Fix soon**
- AGENTS.md signal-to-noise ratio declining (prose bloat, outdated sections)
- MEMORY.md index out of sync with actual memory files
- Skills with bloated descriptions (>200 tokens) or unclear triggers
- Memory files not updated in >14 days despite active sessions
- Critical rules only covered in one layer (should be in AGENTS.md + SOUL.md + relevant skill)

**Incremental - Nice to have**
- Open items with no assigned owner or date
- Skills that could benefit from references/ files to reduce SKILL.md size
- Daily log gaps
- Stale entries in memory files (>90 days, no longer relevant)

## Run Periodically

This health check is most useful when run:
- After a busy sprint or session cluster
- Before briefing a new agent on complex work
- When you notice agent behaviour degrading (forgetting things, ignoring rules)
- Monthly as routine maintenance
