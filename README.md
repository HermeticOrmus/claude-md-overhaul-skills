<p align="center">
  <img src="https://ormus.solutions/mascot/pixellab_liquid_to_terminal.gif" alt="Claude.md Overhaul Skills" width="128" style="image-rendering: pixelated;" />
</p>

<h1 align="center">Claude.md Overhaul Skills</h1>

<p align="center">
  <em>A CLAUDE.md for auditing CLAUDE.md and MEMORY.md files — measures against Anthropic caps, finds bloat, identifies gaps tier-by-tier. Meta-skill for Claude Code memory hygiene.</em>
</p>

<p align="center">
  <a href="https://github.com/HermeticOrmus/claude-md-overhaul-skills/stargazers"><img src="https://img.shields.io/github/stars/HermeticOrmus/claude-md-overhaul-skills?style=flat-square&color=aa8142" alt="Stars" /></a>
  <a href="https://github.com/HermeticOrmus/claude-md-overhaul-skills/blob/main/LICENSE"><img src="https://img.shields.io/github/license/HermeticOrmus/claude-md-overhaul-skills?style=flat-square&color=aa8142" alt="License" /></a>
  <a href="https://github.com/HermeticOrmus/claude-md-overhaul-skills/commits"><img src="https://img.shields.io/github/last-commit/HermeticOrmus/claude-md-overhaul-skills?style=flat-square&color=aa8142" alt="Last Commit" /></a>
  <img src="https://img.shields.io/badge/Claude_Code-aa8142?style=flat-square&logo=anthropic&logoColor=white" alt="Claude Code" />
</p>

---

> **A single `CLAUDE.md` for auditing and improving the Claude Code memory layer. Measures CLAUDE.md and MEMORY.md against Anthropic's documented caps, finds sync conflicts, identifies gaps tier-by-tier.**

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


---

## Part of the Libre Open-Source Stack for Claude Code

This repository is part of a growing family of open-source toolkits for Claude Code.

### Libre suite — comprehensive plugin bundles

- [LibreUIUX-Claude-Code](https://github.com/HermeticOrmus/LibreUIUX-Claude-Code) — UI/UX development (152 agents, 70 plugins, 76 commands, 74 skills)
- [LibreArch-Claude-Code](https://github.com/HermeticOrmus/LibreArch-Claude-Code) — Software architecture and system design
- [LibreCopy-Claude-Code](https://github.com/HermeticOrmus/LibreCopy-Claude-Code) — Technical writing and documentation engineering
- [LibreDevOps-Claude-Code](https://github.com/HermeticOrmus/LibreDevOps-Claude-Code) — DevOps engineering and infrastructure automation
- [LibreEmbed-Claude-Code](https://github.com/HermeticOrmus/LibreEmbed-Claude-Code) — Embedded systems, firmware, and IoT development
- [LibreFinTech-Claude-Code](https://github.com/HermeticOrmus/LibreFinTech-Claude-Code) — Financial technology development
- [LibreGEO-Claude-Code](https://github.com/HermeticOrmus/LibreGEO-Claude-Code) — AI-search optimization (ChatGPT, Perplexity, Gemini, Google AI Overviews)
- [LibreGameDev-Claude-Code](https://github.com/HermeticOrmus/LibreGameDev-Claude-Code) — Game development across Godot, Unity, Unreal
- [LibreMLOps-Claude-Code](https://github.com/HermeticOrmus/LibreMLOps-Claude-Code) — ML engineering and AI operations
- [LibreMobileDev-Claude-Code](https://github.com/HermeticOrmus/LibreMobileDev-Claude-Code) — Mobile app development (Flutter, React Native, native iOS, native Android)
- [LibreSecOps-Claude-Code](https://github.com/HermeticOrmus/LibreSecOps-Claude-Code) — Security operations

### Skills mini-repos — single CLAUDE.md drop-ins

- [vibe-engineer-skills](https://github.com/HermeticOrmus/vibe-engineer-skills) — Direct AI codegen well (hypothesis → scope → validate → reject working-but-wrong)
- [markdown-discipline-skills](https://github.com/HermeticOrmus/markdown-discipline-skills) — Strip AI-slop from markdown (no em dashes, no marketing fluff)
- [shell-safety-skills](https://github.com/HermeticOrmus/shell-safety-skills) — `set -euo pipefail` discipline + 15 failure-mode examples
- [commit-standard-skills](https://github.com/HermeticOrmus/commit-standard-skills) — Ormus Commit Standard v1.0 + commit-msg hook + commitlint
- [unwoke-skills](https://github.com/HermeticOrmus/unwoke-skills) — Strip AI theater (ten sins to eliminate, symmetric engagement)
- [python-conventions-skills](https://github.com/HermeticOrmus/python-conventions-skills) — Modern Python 3.11+ (types, pathlib, async, ruff, mypy, uv)
- [typescript-conventions-skills](https://github.com/HermeticOrmus/typescript-conventions-skills) — TypeScript strict mode, discriminated unions, Result types
- [hermetic-laws-skills](https://github.com/HermeticOrmus/hermetic-laws-skills) — Seven Hermetic Principles applied to engineering
- [riper-workflow-skills](https://github.com/HermeticOrmus/riper-workflow-skills) — Research / Innovate / Plan / Execute / Review systematic dev
- [six-day-cycle-skills](https://github.com/HermeticOrmus/six-day-cycle-skills) — Sustainable shipping cadence with mandatory rest
- [token-optimization-skills](https://github.com/HermeticOrmus/token-optimization-skills) — Claude Code token + context optimization
- [osint-skills](https://github.com/HermeticOrmus/osint-skills) — OSINT research methodology (multi-wave investigative spiral)
- [calcinate-skills](https://github.com/HermeticOrmus/calcinate-skills) — Stage 1 of the Magnum Opus (burn project bloat)
- [session-handoff-skills](https://github.com/HermeticOrmus/session-handoff-skills) — Session handoff + pickup discipline
- [naming-skills](https://github.com/HermeticOrmus/naming-skills) — Product naming methodology (mine the brand's vocabulary)
- [magnum-opus-skills](https://github.com/HermeticOrmus/magnum-opus-skills) — Seven-stage alchemy applied to project transformation

### Template source

- [andrej-karpathy-skills](https://github.com/HermeticOrmus/andrej-karpathy-skills) — the canonical single-file CLAUDE.md pattern (fork of jiayuan_jy's original)

Star the family, not just one — that's how the suite stays coherent.
