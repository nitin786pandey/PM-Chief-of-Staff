# AI-Augmented PM Workflow — Showcase

> **What this is:** A live, working system where Claude (AI) acts as an intelligent co-pilot across my entire product management workflow — connected to real tools, running on a schedule, and maintaining persistent memory across days and weeks.
>
> **What this is not:** A demo or prototype. Every component in this folder reflects how I actually work today.

---

## The Core Idea

Most PMs use AI like a search engine — ask a question, get an answer, move on. I built something different: **a persistent, connected operating system** where AI is woven into the daily rhythm of PM work.

It does three things that most AI setups don't:

1. **Remembers across time** — decisions, risks, open commitments, and customer signals are stored in structured memory files that every daily run reads from and writes back to.
2. **Connects to real tools** — Claude reads and writes across Slack, Jira, Notion, Fireflies, and Google Calendar, not just chat windows.
3. **Runs on a schedule** — morning briefs, evening debriefs, competitive intel harvests, and weekly syntheses fire automatically. I don't prompt them.

---

## System Map

```
┌─────────────────────────────────────────────────────────────────┐
│                        CONNECTED TOOLS                          │
│  Fireflies (meetings) │ Slack │ Jira │ Notion │ Google Calendar │
└────────────────────────────────┬────────────────────────────────┘
                                 │ reads / writes
                                 ▼
┌─────────────────────────────────────────────────────────────────┐
│                         CLAUDE (AI Layer)                       │
│                                                                 │
│  Scheduled Runs:          On-Demand Skills:                     │
│  • Morning Brief (6AM)    • Write spec / PRD                    │
│  • Evening Debrief (6PM)  • Competitive deep dive               │
│  • Competitive Harvest    • Sprint planning                     │
│  • Weekly Synthesis       • Stakeholder update                  │
└────────────────────────────────┬────────────────────────────────┘
                                 │ reads / writes
                                 ▼
┌─────────────────────────────────────────────────────────────────┐
│                          PM OS MEMORY                           │
│                                                                 │
│  Open Loops      Decision Ledger    Risk Register               │
│  Stakeholder     Customer Themes    Customer Insights           │
│  Heatmap         (weekly rollups)   (nightly harvest)           │
└─────────────────────────────────────────────────────────────────┘
```

---

## What's in This Folder

| Section | What it shows |
|---------|--------------|
| [`01-PM-OS/`](./01-PM-OS/overview.md) | The persistent memory system: daily briefs, open loops, decisions, risks |
| [`02-Connected-Tools/`](./02-Connected-Tools/connected-tools.md) | How Claude reads/writes across Slack, Jira, Notion, Fireflies, Calendar |
| [`03-Competitive-Intel/`](./03-Competitive-Intel/overview.md) | Automated daily competitor signal harvesting + weekly synthesis |
| [`SHOWCASE.md`](./SHOWCASE.md) | Single-page narrative document — start here for the full story |

---

## Why I Built This

PM work has a lot of "meta-work" overhead: tracking what you committed to, remembering why a decision was made six weeks ago, keeping up with competitor moves, synthesizing customer calls into themes. That overhead compounds — and it's mostly work that doesn't directly make the product better.

I wanted to eliminate as much of that meta-work as possible so I could spend more time on the actual thinking: what problem to solve, what trade-off to make, how to sequence work.

The result is a system where:
- I start every morning with a brief that already knows what's at risk, what I committed to yesterday, and what customer signals came in overnight.
- Every evening, I capture what happened and the system writes it back to memory — so the next morning brief knows.
- Competitor signals show up in my inbox without me searching for them.
- When I need to write a spec, the AI already has context about the customer themes, open risks, and stakeholder positions.

---

## Technical Overview

| Component | Detail |
|-----------|--------|
| **AI** | Claude (Anthropic) via Cowork desktop app |
| **Scheduling** | Cowork scheduled tasks (cron-style, IST timezone) |
| **Memory** | Markdown files with stable IDs (`L-###`, `D-###`, `R-###`) stored in a local workspace folder |
| **Tool connections** | MCP (Model Context Protocol) integrations for each connected app |
| **Validation** | Python validator (`validate_pm_os.py`) checks schema integrity after each write |
| **Version control** | Git (local) — no secrets committed |

---

## Explore

Start with **[SHOWCASE.md](./SHOWCASE.md)** for the full narrative, or jump directly into any section folder.
