# Agent Smith Analysis

**Project:** pi-monorepo (/home/user/pi)
**Type:** Node.js (`package.json`, npm workspaces)
**Score:** 7.3/10 (first analysis)
**Agent Smith:** v2.5.1
**Date:** 2026-11-09

---

## Summary

The configuration is minimal and safe. The deny rules match the reference list, `.claudeignore` is complete, and the JSON is valid. The main gap is that `CLAUDE.md` tells Claude to read `AGENTS.md`, but `AGENTS.md` is no longer loaded in this session, so the project rules may not apply. The only command is a placeholder.

---

## Pillar Scores

| Pillar | Score | Notes |
|--------|:-----:|-------|
| Security Posture | 9/10 | All 13 reference deny rules present. No hardcoded paths or dates. |
| Instruction Clarity | 7/10 | `CLAUDE.md` is short and clear, but its pointer to `AGENTS.md` is not loaded. |
| Configuration Quality | 9/10 | `settings.json` is valid JSON with a correct `permissions.deny` array. |
| Context Efficiency | 7/10 | `.claudeignore` is complete. No token optimization settings. |
| Command & Extension Design | 4/10 | Only `example.md`, a placeholder with no real command. |
| Hook Safety | N/A | No `hooks.json`. |
| MCP Integration | N/A | No MCP servers configured. |

Weighted score: (9×20 + 7×20 + 9×15 + 7×15 + 4×15) / 85 = 7.3

---

## Findings

### Critical (breaks functionality or security risk)
- None. Validation passed: `settings.json` parses, `deny` is an array, no personal paths, no secrets.

### Important (affects efficiency or maintainability)
- **I1. Project rules may not load.** `CLAUDE.md` says "The authoritative rules are in `AGENTS.md`." This session's notice reports `AGENTS.md` as "no longer present," so Claude does not see the rules unless it reads the file by hand. `AGENTS.md` is 13,186 characters (about 3,300 tokens). Evidence: `CLAUDE.md` L23-24, session notice.
- **I2. `.claude/` is gitignored.** `.gitignore` lists `.claude/`, so `settings.json` and `commands/example.md` are never committed. The team cannot share the deny rules through git. Evidence: `.gitignore`.
- **I3. Placeholder command.** `.claude/commands/example.md` contains template text ("First step", "Begin now."). It is not a working command. Evidence: `.claude/commands/example.md` L1-19.

### Suggestions (improvements, not problems)
- **S1.** `settings.json` has no token settings: `CLAUDE_AUTOCOMPACT_PCT_OVERRIDE`, `MAX_THINKING_TOKENS`, `CLAUDE_CODE_SUBAGENT_MODEL`. Add them only if you want those defaults.
- **S2.** No hooks or MCP servers are configured. This is fine, but no action is needed.

---

## Action Plan

### Option A: Quick Wins (Low Effort)

| # | Action |
|---|--------|
| A1 | Add the three token settings from S1 to `.claude/settings.json` under `env` (values need your choice). |
| A2 | Delete `.claude/commands/example.md`, or replace it with a real command. |

### Option B: Recommended (Medium Effort)

| # | Action |
|---|--------|
| B1 | Fix I1: copy the essential rules from `AGENTS.md` into `CLAUDE.md`, or import `AGENTS.md` if Claude Code supports it. |
| B2 | Fix I2: remove `.claude/` from `.gitignore` if the settings should be shared, or leave it local and say so in `CLAUDE.md`. |

### Option C: Advanced (High Effort)

| # | Action |
|---|--------|
| C1 | None. |

---

## .claudeignore Status

| Check | Status |
|-------|:------:|
| File exists | ✓ |
| `.git/` included | ✓ |
| Covers .gitignore patterns | ✓ |
| Large binaries excluded | ✓ |

---

## Hooks Status

No hooks configured (not required).

## MCP Status

No MCP servers configured (not required).

---

## Content Overview

| File | Lines | Characters | Est. Tokens |
|------|------:|-----------:|------------:|
| `CLAUDE.md` | 29 | 781 | ~195 |
| `AGENTS.md` (not auto-loaded) | 142 | 13,186 | ~3,300 |
| `.claude/settings.json` | 19 | 396 | ~99 |
| `.claude/commands/example.md` | 19 | 227 | ~57 |
| `.claudeignore` | 58 | 767 | ~190 (not loaded into context) |

**Always-loaded total:** about 300 tokens (`CLAUDE.md`). Adding `AGENTS.md` would raise it to about 3,600.

## Cache Efficiency

- **CLAUDE.md size:** about 195 tokens. Verdict: Good (<5K).
- **Volatile markers:** none in `CLAUDE.md`.
- **Duplication:** none. `CLAUDE.md` refers to `AGENTS.md` rather than copying it.

## Wiring Status

No agents, skills, or contexts configured. Wiring checks not applicable.

## Memory Status

No auto-memory found for this project.

---

## Limitations

This analysis covers user-configurable components only. Claude Code's system prompt, built-in tool schemas, and runtime behavior are outside this scope.
