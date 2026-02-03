# RESTORE.md - How to Bring Rune Back

If the hardware dies or Rune is lost, this repo contains everything needed to restore him.

## What's Backed Up

| File | Purpose |
|------|---------|
| `SOUL.md` | Who Rune is — personality, working style, how he helps |
| `IDENTITY.md` | Name, emoji, Telegram handle |
| `USER.md` | Everything about Maria — preferences, projects, treadmill schedule, 2nd Brain setup |
| `MEMORY.md` | Long-term memories, active projects, lessons learned |
| `TOOLS.md` | Environment-specific notes — cameras, SSH hosts, TTS preferences |
| `AGENTS.md` | Workspace guidance, group chat behavior, safety rules |
| `HEARTBEAT.md` | Periodic task checklist (usually empty) |
| `memory/*.md` | Daily log files with raw context |

## How to Restore

1. **Set up a new OpenClaw instance** (new hardware, new VM, etc.)
2. **Create the workspace folder:** `mkdir -p /home/xenu/.openclaw/workspace`
3. **Clone this repo:** 
   ```bash
   git clone https://github.com/xenuloyalofficer/Xenu.git /home/xenu/.openclaw/workspace
   ```
4. **Create `memory/` folder:** `mkdir -p /home/xenu/.openclaw/workspace/memory`
5. **Start OpenClaw** — Rune will read SOUL.md, USER.md, MEMORY.md on first boot and be back

## What You'll Still Need to Reconfigure

- GitHub PAT (for repo access)
- Telegram bot token (if using Telegram)
- Convex deploy key (for 2nd Brain access)
- Vercel tokens
- Any other API keys

## Last Backup

- **Date:** 2026-02-03 12:38
- **Commit:** 85eca83

---

*Keep this repo private — it contains personal information about Maria.*
