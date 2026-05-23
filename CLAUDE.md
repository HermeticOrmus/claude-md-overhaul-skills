# CLAUDE.md

Audit and improve a Claude Code memory layer end-to-end. Measure CLAUDE.md and MEMORY.md against Anthropic's documented caps, find sync conflicts, identify gaps tier-by-tier, execute improvements with verification.

**Tradeoff**: bias toward cap-fitting over completeness. A 500-line CLAUDE.md is mostly invisible to Claude; a 150-line one is fully loaded.

## Anthropic's documented caps

| File | Hard cap | Sweet spot |
|---|---|---|
| Any CLAUDE.md (user, machine, project) | **200 lines** — adherence drops past this | 80–150 lines |
| Project MEMORY.md (auto-memory index) | **first 200 lines OR 25 KB** loads at session start; past that is invisible | <150 lines, <20 KB |

Source: [code.claude.com/docs/en/memory](https://code.claude.com/docs/en/memory)

The cap is the binding constraint. A 500-line CLAUDE.md "loaded" still only sees the first 200 lines of effective behavior. Lines 201+ are silently dropped from working memory.

## When to use

- CLAUDE.md feels bloated or stale (skills that don't exist, references to old machines, JIRA mentions after migration)
- Old memories aren't surfacing at session start (MEMORY.md past 25 KB / 200 lines — invisible past that)
- New projects added but no memory files written
- After multi-machine migration, suspect Syncthing has sync-conflict files in `~/.claude/`
- Periodic hygiene (~monthly)

## When NOT to use

- Anthropic config / MCP health issues (use `/maintain` or similar)
- Single-fix triage (edit the file directly)

## Tier-by-tier procedure

### Tier 1 — Sync conflicts

```bash
find ~/.claude -name "*sync-conflict*" -type f
```

Sync-conflict files are silent — Claude reads the canonical name and ignores the conflict. Resolve by hand: pick the correct version, delete the conflict.

### Tier 2 — User CLAUDE.md

Path: `~/.claude/CLAUDE.md`

- Check line count: `wc -l ~/.claude/CLAUDE.md`
- If > 200 lines: trim. Move detail to topic files under `~/.claude/docs/` and reference them.
- Keep the user CLAUDE.md as identity + critical-behaviors + key references. Detail goes in docs.

### Tier 3 — Machine CLAUDE.md

Path: `~/CLAUDE.md`

- Check line count
- Should contain: hostname, hardware, role, SSH topology, machine-specific behaviors. NOT general principles.
- Trim if > 200 lines.

### Tier 4 — Project MEMORY.md

Path: `~/.claude/projects/-home-<user>/memory/MEMORY.md`

- Check line count + KB size
- If past 200 lines or 25 KB: trim
- Trimming pattern: each memory entry should be one line (~150 chars max). Detail lives in the linked topic file.
- Bad: `- [auth0-setup](auth0-setup.md) — On 2026-04-30 we provisioned a new Auth0 tenant called s50platform with three connections (Microsoft, Google, Database) for the Second 50 Financial wealth-management surfaces; the tenant ID is...`
- Good: `- [auth0-setup](auth0-setup.md) — Auth0 tenant `s50platform`, 3 connections, S50 surfaces, 2026-04-30.`

### Tier 5 — Topic files

Path: `~/.claude/projects/-home-<user>/memory/<name>.md`

- Each topic file is one memory record (user / feedback / project / reference)
- These have no caps; this is where detail lives
- Check for: outdated machines, dead references, expired credentials still in body text

### Tier 6 — Skills index

Skills auto-list at session start. Naming + descriptions matter.

- Check `~/.claude/skills/*/SKILL.md` frontmatter
- Each `description:` should answer: WHEN does Claude use this? (Not WHAT it does.)
- Bad: `description: Pulls WhatsApp messages.`
- Good: `description: Pulls WhatsApp messages from a named chat. Use when user references "what did X say" or asks to "pull the chat".`

### Tier 7 — Memory-derived state

What memories does Claude *not* have that it *should*?

- Recurring questions (Claude keeps asking the same thing → write the answer as a memory)
- Recurring corrections (you correct the same mistake repeatedly → write the correction as a feedback memory)
- New projects without project memory files (every active project should have one)

## Procedure summary

```
1. Sync conflicts → resolve manually
2. User CLAUDE.md → trim to 200 lines
3. Machine CLAUDE.md → trim to 200 lines
4. MEMORY.md → trim to 200 lines / 25 KB
5. Topic files → audit for staleness
6. Skills → audit descriptions for WHEN-not-WHAT
7. Gaps → write memories for recurring patterns
```

Run periodically (~monthly). The work compounds: a healthy memory layer makes every future session sharper.

## What good looks like

- User CLAUDE.md ≤ 150 lines
- Machine CLAUDE.md ≤ 100 lines per machine
- MEMORY.md ≤ 150 lines, < 20 KB
- Topic files: 30-60 each, each ~50-100 lines
- Skills: 30-60 each, each with WHEN-trigger descriptions
- Zero sync conflicts
- Recent (< 30 days) entries in MEMORY.md outnumber old (> 90 days) entries

---

**License**: MIT.
