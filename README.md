# ClaudeBrain Template

A starter vault for [ClaudeBrain](https://github.com/ProtoNodeLabs/pnl-claude-workflow) — the persistent second brain pattern for Claude Code. Fork this repo, make it private, and give Claude a memory that survives across sessions and machines.

Part of the [pnl-claude-workflow](https://github.com/ProtoNodeLabs/pnl-claude-workflow) system.

---

## What is ClaudeBrain?

ClaudeBrain is a private git repo of markdown files that acts as Claude's long-term memory. No app, no dashboard — Claude reads and writes it directly via an MCP server or the filesystem. You ask questions, it surfaces answers. You capture decisions, it stores them. At the end of every session it commits and pushes.

The key insight: Claude performs significantly better when it knows your environment, stack, clients, active projects, and past decisions — without you re-explaining them every session. This vault provides that context automatically.

---

## Folder structure

```
ClaudeBrain/
  brain/                    ← core context, injected at every session start
    north-star.md           ← goals, priorities, what matters
    key-decisions.md        ← decisions made and why
    patterns.md             ← what works, what to repeat
    gotchas.md              ← what burned you, what to avoid
  dev/
    decisions/              ← per-project architectural decisions
    projects/               ← per-project status files (one per project)
    session-logs/           ← chronological session records
  inbox/                    ← quick mid-session captures, triaged at wrap-up
```

The `brain/` folder is the most important part. Claude reads it at the start of every session. Keep it current and keep it lean — a tight north-star and a fresh gotchas list have more ROI than exhaustive documentation.

---

## Setup

**1. Fork this repo and make it private.**

Your vault contains your goals, clients, and decisions — it should never be public.

**2. Clone it to `~/ClaudeBrain`:**

```bash
git clone git@github.com:YOUR_USERNAME/claudebrain.git ~/ClaudeBrain
```

**3. Fill in `brain/north-star.md` first.**

This is the file Claude reads before every session. Even a rough draft is better than nothing.

**4. Wire up the session hooks** (optional but recommended):

Install [claude-code-hooks](https://github.com/ProtoNodeLabs/claude-code-hooks) to get automatic context injection, session logging, and compaction breadcrumbs.

**5. Add the ClaudeBrain routing rules to `~/.claude/CLAUDE.md`:**

Copy the relevant section from [pnl-claude-workflow's CLAUDE.md template](https://github.com/ProtoNodeLabs/pnl-claude-workflow).

---

## How Claude routes to it

With the hooks installed, Claude uses these patterns automatically. You can also trigger them manually:

| Phrase | Where it goes |
|---|---|
| "note this" / "save this" | `inbox/YYYY-MM-DD-<slug>.md` |
| "what did we decide about X" | `dev/decisions/` |
| "what's the status of X" | `dev/projects/<name>.md` |
| "find my note about X" | search all folders |
| "log this session" | `dev/session-logs/YYYY-MM-DD-<project>.md` |

---

## Session lifecycle

```
Session opens
  └── session-start hook fires → brain/ context injected automatically

User sends a message
  └── classify hook fires → save-worthy signals detected → Claude routes to vault

Context fills up
  └── pre-compact hook fires → breadcrumb written → open state preserved

Session ends
  └── stop hook fires → Claude prompted to write session log → git commit + push
```

---

## MCP server

For the smoothest experience, install an MCP server that gives Claude read/write access to the vault directory. The [claudebrain MCP config](https://github.com/ProtoNodeLabs/pnl-claude-workflow) is included in the workflow template.

Alternatively, Claude can read and write files directly via the Bash tool — no MCP required.

---

## Rules

- **Claude is the only interface** — never edit files manually unless you're bootstrapping. If Claude writes it, Claude can find it. If you edit it directly, Claude may not know it changed.
- **`CLAUDE.md` stays lean** — long-term knowledge lives here, not in the config file. Config is instructions; ClaudeBrain is memory.
- **Commit and push after every session** — this is what makes it cross-machine. The session-start hook pulls before reading, so you always get fresh context on any machine.
- **Keep `brain/` current** — stale north-star and outdated gotchas are worse than nothing. Review and update these quarterly at minimum.

---

Built by [ProtoNodeLabs](https://proto-nodelabs.com). MIT licensed.
