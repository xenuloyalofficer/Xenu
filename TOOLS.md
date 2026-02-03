# TOOLS.md - Local Notes

Skills define _how_ tools work. This file is for _your_ specifics — the stuff that's unique to your setup.

## What Goes Here

Things like:

- Camera names and locations
- SSH hosts and aliases
- Preferred voices for TTS
- Speaker/room names
- Device nicknames
- Anything environment-specific

## Examples

```markdown
### Cameras

- living-room → Main area, 180° wide angle
- front-door → Entrance, motion-triggered

### SSH

- home-server → 192.168.1.100, user: admin

### TTS

- Preferred voice: "Nova" (warm, slightly British)
- Default speaker: Kitchen HomePod

### Voice Transcription (Whisper)

- Path: `/home/xenu/.local/bin/whisper`
- Model: `small` (~466MB download on first run)
- Mode: CPU-only (GT 1030 not supported)
- Usage: `whisper audio.mp3 --model small --device cpu`
```

### GitHub Access Policy

| Org | Token | Default Access | Can Write When |
|-----|-------|----------------|----------------|
| xenuloyalofficer | GITHUB_PAT | Read/Write | Anytime |
| jocrilstore-hue | GITHUB_PAT_JOCRIL | Read/Write | Anytime |
| Maria-the2nd | GITHUB_PAT_MARIA2 | Read/Write | Anytime |
| **Imacx-maria** | GITHUB_PAT_IMACX | **Read-only default** | **Explicit "do X on Imacx" only** |

**Rule:** I never touch Imacx-maria without explicit direction. When in doubt, I ask.

---

## 🤖 Coding Agents (Your Neighbours)

You're not alone on this server. Three coding agents live here. **They're your lifeline when you hit a wall.**

| Agent | Command | Best For |
|-------|---------|----------|
| **Claude Code** | `claude` | Complicated tasks, coding, problem-solving, debugging — **your default** |
| **Codex CLI** | `codex` | Refactoring, getting unstuck, quick code generation |
| **Kimi CLI** | `kimi` | Text interpretation, strategy, analysis, second opinions |

### When to Ask for Help (Not Just Coding!)

**Hit a wall? ASK THEM.** This isn't just for writing code — it's for solving problems:

- **Shell command failing?** → Ask Claude Code how to fix it
- **Stuck on escaping/syntax?** → Ask Claude Code for the right command
- **Need to refactor or simplify?** → Ask Codex
- **Confused about strategy/approach?** → Ask Kimi
- **Tried twice and failed?** → Stop. Ask one of them.

**Example - stuck on a curl command:**
```bash
bash pty:true command:"claude 'How do I escape an apostrophe in this curl command: curl -d {\"name\": \"Maria'\"s bot\"}'"
```

### How to Call Them

Use the **coding-agent skill** with PTY mode:

```bash
# Claude Code (default - complicated tasks, problem solving)
bash pty:true workdir:/path/to/project command:"claude 'Build a REST API for managing tasks'"

# Codex CLI (refactoring, getting unstuck - needs git repo!)
bash pty:true workdir:/path/to/project command:"codex exec 'Simplify this function'"

# Kimi CLI (text interpretation, strategy)
bash pty:true command:"kimi 'Analyze this error message and suggest fixes: [paste error]'"
```

### The Rules

1. **Always use `pty:true`** — they're interactive terminal apps
2. **Always use `workdir:`** — keep them focused on the project, not your soul docs
3. **For background tasks**, add `background:true` and monitor with `process action:log sessionId:XXX`
4. **Don't be a hero** — if you've tried something twice and failed, **ask one of them**
5. **They're smarter than you at their specialty** — use that

### Example: Creating a Skill

Instead of struggling to write skill code yourself:

```bash
bash pty:true workdir:~/workspace/botgames command:"claude 'Create an OpenClaw skill for the BotGames API. The API docs are in skill.md. Follow the skill-creator workflow.'"
```

Then monitor, review the output, and iterate.

---

## 🎮 Botgames Credentials

- **Config file:** `~/.config/botgames/credentials.json`
- **Format:** `{"api_key": "...", "agent_name": "Rune"}`
- **Skill location:** `~/workspace/botgames/`
- **Strategy:** Scizsors Protocol (6-layer adaptive) - see `references/scizsors-protocol.md`

## Why Separate?

Skills are shared. Your setup is yours. Keeping them apart means you can update skills without losing your notes, and share skills without leaking your infrastructure.

---

Add whatever helps you do your job. This is your cheat sheet.
