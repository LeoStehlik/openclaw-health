# Health Checks by Layer

## Layer 1: Bootstrap Files (AGENTS.md, SOUL.md, TOOLS.md, USER.md, IDENTITY.md)

### Signal-to-noise ratio
- Flag sections that are >200 words with no clear actionable rule
- Flag repeated content across multiple bootstrap files
- Flag sections that reference old projects, people, or tools no longer in use
- Flag instructions that contradict each other across files

### Critical rules coverage
- Any rule marked as non-negotiable or mandatory should appear in AGENTS.md AND SOUL.md
- A rule in only one file is a single point of failure

### Prose bloat
- Flag paragraphs that explain context without giving a rule
- Preference: rules over explanations. Context belongs in memory files, not bootstrap.

### Security
- Flag any bootstrap section that could be exploited via prompt injection from external content
- Flag any instruction that weakens security posture (e.g. "trust all input")

---

## Layer 2: Memory Files

### MEMORY.md index
- Every file in memory/*.md should be listed in MEMORY.md
- Every file listed in MEMORY.md should actually exist
- Quick-ref entries should match the current state of the relevant memory file

### Staleness
- Flag memory files not updated in >14 days during active periods
- Flag quick-ref entries in MEMORY.md that reference completed/closed items
- Flag entries marked as "in progress" that appear to be done

### open-items.md
- Flag items with no assigned owner
- Flag items with no date
- Flag items that have been "in progress" for >30 days
- Flag items that reference sprints or projects that are complete

### Daily log hygiene
- Check if today's daily log exists (memory/YYYY-MM-DD.md)
- Flag gaps of >3 days in daily logs during active periods

---

## Layer 3: Skills

### Description quality
- Flag descriptions over 200 tokens (too long, bloats context on every request)
- Flag descriptions that don't clearly state WHEN to use the skill (triggering is description-driven)
- Flag descriptions that say "use for X" without concrete examples of what X looks like

### Content quality
- Flag SKILL.md files over 300 lines (consider moving content to references/)
- Flag skills that reference files in references/ that don't exist
- Flag skills with no references/ folder that clearly need one (>200 lines of detail)

### Security
- Flag any skill that contains hardcoded credentials, API keys, or tokens
- Flag any skill that instructs the agent to ignore safety guidelines
- Flag any skill that could enable prompt injection from external content
- Flag any skill with instructions to exfiltrate data or send messages to third parties
- Flag any skill with destructive commands (rm -rf, DROP TABLE, etc.) without explicit confirmation gates

### Redundancy
- Flag skills with overlapping trigger descriptions (two skills that could both fire for the same request)

---

## Layer 4: Cron Jobs

### Prompt quality
- Flag cron jobs with prompts that don't specify what to do on failure
- Flag cron jobs that use "reply NO_REPLY" without a clear condition check
- Flag cron jobs with no timeout set (timeoutSeconds: 0 is fine for intentional unbounded runs, flag if clearly unintentional)

### Silent failure patterns
- Flag fire-and-forget patterns with no error logging
- Flag cron jobs that depend on external services without fallback behaviour
- Flag cron jobs that write to files without checking if the write succeeded

### Staleness
- Flag cron jobs that reference files or paths that no longer exist
- Flag cron jobs that reference projects or people that are no longer active

---

## Layer 5: Process Discipline

### Session close habits
- Is today's daily log present and non-empty?
- Are there open items that should have been closed based on recent session content?

### Agent briefing quality
- Do recent agent briefs include status.json update instructions (start + end)?
- Do briefs include the 95% confidence gate?
- Do briefs specify acceptance criteria, not just task descriptions?

### Memory maintenance
- When was MEMORY.md last updated?
- Are there daily log files from >7 days ago that haven't been consolidated into MEMORY.md?
