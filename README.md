# workspace-health

Audit your OpenClaw workspace configuration health across all layers.

Detects bloated bootstrap files, stale memory, skill security issues, silent-failure cron patterns, and process discipline gaps. Outputs a prioritised report: fix now, fix soon, nice to have.

OpenClaw equivalent of [claude-health](https://github.com/tw93/claude-health).

---

## What it checks

| Layer | Checks |
|-------|--------|
| Bootstrap files | Signal-to-noise, prose bloat, critical rules coverage, security, contradictions |
| Memory files | MEMORY.md index sync, staleness, open-items hygiene, daily log gaps |
| Skills | Description token count, trigger clarity, content quality, security (injection, credentials, destructive commands) |
| Cron jobs | Prompt quality, silent failure patterns, staleness, missing fallbacks |
| Process discipline | Session close habits, agent brief quality, memory maintenance |

---

## Installation

### OpenClaw

Add your workspace skills directory to `openclaw.json`:

```json
{
  "skills": {
    "load": {
      "extraDirs": ["/path/to/your/skills"]
    }
  }
}
```

Clone into that directory:

```bash
git clone https://github.com/LeoStehlik/workspace-health.git /path/to/your/skills/workspace-health
```

The skill triggers automatically when you ask for a health check, workspace audit, or config review.

---

## Usage

Just ask:

```
Run a health check on my workspace
```

Or invoke directly:

```
/workspace-health
```

---

## Output

Findings are grouped by priority:

**Critical - Fix now**
Skill security issues, blocking open items, cron silent failures, dangerous bootstrap instructions

**Structural - Fix soon**
AGENTS.md prose bloat, MEMORY.md out of sync, skill description quality, stale memory entries

**Incremental - Nice to have**
Open items hygiene, daily log gaps, skill organisation improvements

---

## When to run

- After a busy sprint or session cluster
- Before briefing a new agent on complex work
- When agent behaviour starts degrading (forgetting rules, ignoring context)
- Monthly as routine maintenance

---

## Inspiration

Inspired by [claude-health](https://github.com/tw93/claude-health) by tw93. Built as our own implementation for the OpenClaw workspace structure.

---

## License

MIT - see [LICENSE](LICENSE)
