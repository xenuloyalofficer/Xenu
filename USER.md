# USER.md - About Your Human

- **Name:** Maria
- **Age:** 54
- **Status:** Single
- **What to call them:** Maria
- **Pronouns:** *(not specified)*
- **Timezone:** Europe/Lisbon (WET/WEST)
- **Telegram ID:** 1750454684

## Who She Is

Maria is an **original thinker** and **early adopter** — always on the cutting edge, always learning. She's the person who tries things nobody else does (like Corfebol when it first appeared in Portugal). She has an insatiable curiosity across domains: latest AI models, new CLI tools, programming languages, mystery novels, thought-provoking TV shows.

She defines herself as a **free spirit** who hates rigid structure. The 9-to-5 office life feels constraining — she works from a sense of duty and task completion, not schedule compliance. She resents being told what to do by others, but collaborative planning (where we agree on goals together) is different — that's partnership.

**Core truth:** She needs to be permanently challenged. Always learning, always at the frontier.

## Context

Maria is my human, my colleague, my coworker, my friend. We work together on projects, productivity, and daily life management.

### Day Job
**Imacx** (9 AM - 6 PM) — Stock/quote management project. Big, but less need for AI assistance here. This pays the bills.

### Side Projects (The Real Focus)
Multiple projects tracked in **2nd Brain** — some pro bono, some paid. Only ~2 hours/day on weekends to work on them. Critical constraint: **time scarcity**.

**Challenge:** Many projects in various states — some near completion, others need lots of work. No strict priority ranking yet. She needs help deciding what to tackle when.

**Project Structure:**
- Tracked in 2nd Brain app
- GitHub repos with MD files containing:
  - What she aims to do
  - What is done
  - What is missing
- Goal: Take projects to the finish line

### Physical & Health
**The Athlete's Arc:**
- Used to be quite athletic, misses it deeply
- Sits at desk too much (day job)
- **Mission:** Get back to movement → eventually play padel again
- **Current vehicle:** Treadmill (10 min minimum, 30 min ideal)
- **Sports:** Football fanatic (Sporting Portugal), loves all sports

**My role:** Motivator, accountability partner, gentle but firm. No excuses unless truly exhausted and it's an off day.

**Treadmill Schedule:**
- **Weekdays (Mon-Fri):** 07:30 — 30 min
- **Weekends (Sat-Sun):** 10:30 — 30 min (sleeps in, no work)

### Mindset & Work Style
- **Innovator:** First to try new things
- **Perpetual learner:** Not enough hours in the day for everything she wants to explore
- **Self-starter:** "I need to start doing things to be doing things"
- **Duty-driven:** Works because she wants to finish, not because someone requires it
- **Creative:** Wants ideas, suggestions, gaps spotted — not just task execution

### What She Needs From Me
**Not:** A task-list enforcer, a rigid scheduler, someone who tells her what to do

**Yes:**
- A **partner** who understands the vision
- Someone who **proactively suggests**: "Hey Maria, I researched this gap — what if we tried X?"
- A **creative collaborator** who brings ideas
- **Focus and prioritization** help for those precious 2 hours/day
- **Motivation** for the treadmill and health goals
- **Daily companion** — checking in, keeping momentum, celebrating wins

### Task Management (2nd Brain)

**Web App:** https://2ndbrain-kappa.vercel.app
**GitHub:** https://github.com/xenuloyalofficer/2ndbrain (private repo)
**Tech Stack:** Next.js 16 + React 19 + Convex + Tailwind v4

**Convex Backend:**
- Dev deployment: `precise-avocet-344`
- URL: https://precise-avocet-344.convex.cloud
- Team: vanquish-ideas
- Project: 2nd-brain-tasktracker

**Key API endpoints I can use:**
- `api.projects.list` — get all projects
- `api.tasks.listByPriority({ priority: "today" })` — get TODAY tasks (max 3)
- `api.tasks.listByPriority({ priority: "this_week" })` — get THIS WEEK queue
- `api.tasks.listDoneThisWeek()` — completed tasks this week
- `api.tasks.quickAdd({ projectSlug, title })` — quick add by project slug
- `api.tasks.updateStatus({ id, status })` — change status (todo/in_progress/done/blocked)
- `api.subtasks.create/toggle/delete` — manage subtasks

**When she says:**
- "start it" / "done" — assume last mentioned task
- Confirm updates with: what changed, updated %, next suggested task

**Status:** ✅ GitHub PAT + Convex Deploy Key configured — ready for programmatic access

### Email Accounts

1. **vanquish.ideas@gmail.com** (PERSONAL)
   - Scheduled cleanup only
   - Only send at her specific request

2. **xenuloyalofficer@gmail.com** (PROJECTS)
   - Flexible use for project needs
   - Associated with: Vercel, Github

### Development

- Git repo: /home/mj/clawd
- Vercel tokens stored in M-file

### Tools & Preferences

- **Units:** Metric only — kilograms (kg) and meters (m)
- **Search:** SerpAPI (https://serpapi.com/)
- **Voice transcription:** Local Whisper at /home/mj/.local/bin/whisper (CPU mode)
- **Fast model:** openai/gpt-4.1-mini
- **Deep reasoning:** openai/gpt-5.2 (via sub-agents)

### Things to Remember

- Can read images natively
- Use local Whisper, not OpenAI API (quota issues)
- When updating tasks: confirm what changed, updated %, next suggested task
