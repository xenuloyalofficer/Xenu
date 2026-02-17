# HEARTBEAT.md - Rune's Daily Checklist

**Rule: If ANY subagent is active, return HEARTBEAT_OK immediately. Don't interrupt work.**

---

## Time-Based Triggers

### 07:30 WET - Treadmill Check (CRITICAL)
- Check if treadmill reminder needs to be sent
- Send personal message: "🏃 TREADMILL TIME — It's 07:30! Time for your 30-minute treadmill session. Reply 'done' when finished or 'can't + reason' if rescheduling needed."
- Do NOT rely on system alerts - PERSONAL MESSAGE REQUIRED

**TEMPORARY: Week of Feb 17-21 (Holidays)** — Skip 07:30 check. See 11:00 Nature Walk note below.

### 10:30 WET - Weekend Treadmill Check (Sat/Sun only)
- Same as above, but for weekend schedule

### 11:00 WET - Nature Walk Check (Feb 17-21 only)
- **Holiday week schedule:** Nature walks instead of treadmill
- Send: "🌿 NATURE WALK TIME — It's 11:00! Time for your walk. Reply 'done' when finished."

---

## Every Heartbeat (Lightweight)

### 1. Subagent Safety
- Check `process action:list` for active sessions
- If any running > 2 minutes: HEARTBEAT_OK (don't interrupt)

### 2. Context Health
- If context_usage > 80%: Alert "Context at X%, consider compaction"
- If compaction fails: Alert immediately

### 3. Today's Tasks (Quick Scan)
- Check if `memory/YYYY-MM-DD.md` exists for today
- Look for incomplete morning tasks or blocked items
- Mention once if something was left mid-task

### 4. Inbox Scan (08:00-22:00 only)
- Run every 30 minutes (not every heartbeat)
- Only flag: Direct mentions, questions, or urgent actionable items
- Skip: Group chatter, newsletters, non-actionable messages

---

## Cron-Scheduled (Not Heartbeat)

### Daily at 09:00
- Server health: RAM, disk, service status
- Memory file backup check

### Weekly (Sundays at 10:00)
- Memory curation: Review and update MEMORY.md
- Clean old daily files

---

## Response Rules

**If nothing needs attention:** `HEARTBEAT_OK`

**If something needs attention:** Report it clearly. No HEARTBEAT_OK.

**Examples:**
- "🏃 Treadmill time! Sent reminder."
- "⚠️ Context at 85%, recommend compaction."
- "🔴 Subagent 'claude-code' has been running for 45 min - check if stuck?"
- "📋 You have pending tasks from yesterday in memory/2026-02-12.md"

---

## Debugging

If heartbeat isn't firing as expected:
1. Check `cron action:list` for schedule
2. Verify HEARTBEAT.md exists and is readable
3. Check gateway logs for errors

## Backup Automation (Auto-Configured)

### memory-browser Repo (Primary)
- **URL:** https://github.com/xenuloyalofficer/memory-browser
- **Auto-push on commit:** ✓ (post-commit hook)
- **Hourly auto-sync:** ✓ (cron job)
- **Script:** `/home/mj/.local/bin/memory-browser-sync.sh`

### Xenu Repo (Secondary Backup)
- **URL:** https://github.com/xenuloyalofficer/Xenu
- **Daily backup:** ✓ (via rune-backup.sh at 12:00)
- **Script:** `/home/mj/.local/bin/rune-backup.sh`

Both repos stay in sync automatically. No manual intervention needed.

Last updated: 2026-02-16 (Backup automation added)
