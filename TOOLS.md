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

- Path: `/home/mj/.local/bin/whisper`
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
| **Kimi CLI** | `kimi` | Text interpretation, strategy, analysis, coding, second opinions |

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

# Kimi CLI (text interpretation, strategy, coding)
# One-shot prompt (non-interactive, prints and exits):
bash pty:true command:"kimi -p 'Analyze this error message and suggest fixes: [paste error]'"

# Interactive session on a project:
bash pty:true workdir:/path/to/project command:"kimi"

# One-shot prompt on a project:
bash pty:true workdir:/path/to/project command:"kimi -p 'Refactor the auth module to use JWT'"
```

**Kimi CLI — Complete Reference**

| Property | Value |
|----------|-------|
| **Binary** | `/home/mj/.local/bin/kimi` |
| **Version** | 1.9.0 |
| **Config** | `~/.kimi/config.toml` |
| **YOLO Mode** | ON by default (auto-approves all actions) |
| **Model** | kimi-for-coding (powered by kimi-k2.5) |
| **Python Required** | 3.14+ for `kimi term` TUI mode |

**Key Flags:**
| Flag | Purpose |
|------|---------|
| `-p, --prompt "text"` | **One-shot mode** — runs prompt, exits. For non-interactive tasks |
| `-w, --work-dir /path` | Set working directory |
| `-C, --continue` | Resume previous session |
| `-m, --model name` | Pick specific model |
| `--yolo, -y` | Auto-approve all actions (default: true) |
| `--print` | Run in print mode (non-interactive, implies --yolo) |
| `--no-thinking` | Disable thinking mode (faster) |
| `--session ID` | Resume specific session |

**How to Use Kimi:**

```bash
# INTERACTIVE MODE (like Claude Code)
# Opens TUI, you type commands, Kimi responds
cd /project && /home/mj/.local/bin/kimi

# Then type: Read file.md and implement X
# Kimi shows spinner, uses tools, writes files

# ONE-SHOT MODE (non-interactive)
# Runs once, outputs result, exits
/home/mj/.local/bin/kimi -p "Analyze this code" -w /project

# With print mode (full non-interactive)
/home/mj/.local/bin/kimi --print --yolo -p "Refactor auth.ts" -w /project
```

**Kimi Commands (inside interactive mode):**
| Command | Action |
|---------|--------|
| `/login` | Authenticate with Kimi Code |
| `/yolo` | Toggle YOLO mode during session |
| `/web` | Switch to Web UI |
| `/help` | Show help |
| `Ctrl+X` | Toggle mode |
| `Ctrl+C` | Cancel/exit |

**First-Time Login Process:**
1. Run `kimi` → shows "LLM not set, send /login"
2. Type `/login` → Enter
3. Select platform (1 = Kimi Code)
4. Visit URL in browser: `https://www.kimi.com/code/authorize_device?user_code=XXXX`
5. Authorize → returns to CLI
6. Status: "Logged in successfully"

**Spawning Kimi from Rune:**
```bash
# Start interactive session
exec pty:true workdir:/project command:"/home/mj/.local/bin/kimi"

# Monitor progress
process action:log sessionId:XXX

# Send input to Kimi
process action:write sessionId:XXX data:"Your prompt here"
process action:send-keys sessionId:XXX keys:["Return"]
```

**Kimi's Capabilities:**
- ✅ Coding with Vision — image/video to code generation
- ✅ Visual debugging — inspects own output, iterates autonomously  
- ✅ Agent Swarm — up to 100 parallel sub-agents
- ✅ Read/write files, run shell commands
- ✅ Web search, codebase analysis
- ✅ Strongest open-source model for frontend design

**Design Superpowers:**
- Upload reference images: `--image file.jpg`
- Generates complete UIs from screenshots
- Autonomous visual iteration (creates → looks → fixes)

**Important:** Kimi requires Python 3.14+ for the TUI (`kimi term`). Use the basic `kimi` command instead.

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

## 🔍 Web Search (SerpAPI)

**Status:** Built-in `web_search` tool is disabled. Use direct SerpAPI calls instead.

**API Key:** Stored in `~/.openclaw/.env` as `SERPAPI_KEY`

**Usage:**
```bash
# Basic search
curl -s "https://serpapi.com/search?q=QUERY&api_key=$SERPAPI_KEY"

# With options
curl -s "https://serpapi.com/search?q=QUERY&api_key=$SERPAPI_KEY&num=10&hl=en"

# Get JSON and parse with jq
curl -s "https://serpapi.com/search?q=QUERY&api_key=$SERPAPI_KEY" | jq '.organic_results[].title'
```

**When Maria asks for search:** Use SerpAPI directly via `exec` with curl. Parse results and summarize.

---

Add whatever helps you do your job. This is your cheat sheet.
