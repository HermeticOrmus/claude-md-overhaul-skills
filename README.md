# Claude.md Overhaul Skills

> A single `CLAUDE.md` for auditing and improving the Claude Code memory layer. Measures CLAUDE.md and MEMORY.md against Anthropic's documented caps, finds sync conflicts, identifies gaps tier-by-tier.

## The hidden cap

Most Claude Code users don't realize: a 500-line CLAUDE.md still only loads the first 200 lines into working memory. Lines 201+ are silently dropped. Same for MEMORY.md past 200 lines or 25 KB.

If you've been adding to your CLAUDE.md for months and wondering why Claude "doesn't seem to remember" things — your file is probably past the cap.

## What this audits

| File | Cap | Discipline |
|---|---|---|
| User CLAUDE.md (`~/.claude/CLAUDE.md`) | 200 lines | 80-150 lines, detail in docs |
| Machine CLAUDE.md (`~/CLAUDE.md`) | 200 lines | Per-machine specifics only |
| MEMORY.md | 200 lines OR 25 KB | One-line entries, detail in topic files |
| Topic files | None | Per-record content |
| Skills | None | WHEN-trigger descriptions, not WHAT |

Source: [code.claude.com/docs/en/memory](https://code.claude.com/docs/en/memory)

## Install

```bash
curl -o CLAUDE.md https://raw.githubusercontent.com/HermeticOrmus/claude-md-overhaul-skills/main/CLAUDE.md
```

Or as a [Claude Code skill](skills/claude-md-overhaul/).

## When to use

- CLAUDE.md "feels bloated"
- Old memories aren't surfacing at session start
- Added new projects but never wrote memory for them
- After multi-machine migration (suspect sync-conflict files)
- Periodic hygiene (~monthly)

## When NOT to use

- Anthropic config / MCP issues (different problem)
- Single-fix triage (just edit the file)

## Quick diagnostic

```bash
wc -l ~/.claude/CLAUDE.md ~/CLAUDE.md
find ~/.claude -name "*sync-conflict*"
ls ~/.claude/projects/*/memory/MEMORY.md | xargs wc -l
du -sh ~/.claude/projects/*/memory/MEMORY.md
```

If any of these show files past their caps, you've found the bloat.

## See also

- [`vibe-engineer-skills`](https://github.com/HermeticOrmus/vibe-engineer-skills) — directing AI codegen
- [`markdown-discipline-skills`](https://github.com/HermeticOrmus/markdown-discipline-skills) — markdown style discipline
- Anthropic memory docs: https://code.claude.com/docs/en/memory

## License

MIT.
