# How I Use AI to Run My PM Workflow

**A walkthrough of a live, connected, scheduled AI operating system for product management**

---

## The Problem I Was Solving

Product management has two types of work: the actual thinking (what to build, why, for whom, in what order) and the meta-work that surrounds it (tracking commitments, updating stakeholders, reviewing competitor moves, synthesizing customer calls, maintaining documentation).

The meta-work is necessary but doesn't make the product better. And it compounds — miss a day of it and you're catching up on three.

I wanted to eliminate as much of the meta-work as possible. Not by ignoring it, but by having a system handle it automatically so I could focus on the thinking.

The result is what I call **PM OS** — a persistent, connected, scheduled AI operating system that runs alongside my workday.

---

## What It Does (in one paragraph)

Every morning, a brief is waiting for me — already pulled from my open commitments, active risks, past decisions, and overnight customer call transcripts. Throughout the day, I can ask Claude to search Slack, create Jira tickets from specs, update Notion pages, or do a competitive deep dive. Every evening, a debrief runs automatically — it compares what I planned against what happened, updates my memory files, and sets up the next morning brief. Meanwhile, competitor signals are harvested every weekday morning and synthesized every Friday. I don't prompt any of this. It runs on a schedule.

---

## The Architecture

### Layer 1 — Connected Tools

Claude has live read/write access to the tools I use every day:

| Tool | What Claude reads | What Claude writes |
|------|------------------|--------------------|
| **Fireflies** | Meeting transcripts + AI summaries | — |
| **Slack** | Channel messages, threads, search | Drafted messages (with my approval) |
| **Jira** | Issue status, epic structure, search | New tickets, comments, status updates |
| **Notion** | Project pages, PRDs, docs | Status updates, new content |
| **Google Calendar** | Today's events, availability | Meeting suggestions |

Each connection uses **MCP (Model Context Protocol)** — a standardized protocol that keeps credentials secure and actions auditable.

### Layer 2 — Scheduled Runs

Four tasks fire automatically without any prompt from me:

**Fireflies Harvest (1 AM nightly)**
Pulls the previous day's meeting transcripts from Fireflies. Extracts customer signals — pain points, feature requests, sentiment patterns. Writes structured summaries into `Customer Insights — Latest.md`. Every morning brief reads this file.

**Morning Brief (6 AM weekdays)**
A read-only run. Reads: Open Loops (my commitments), Risk Register, Decision Ledger, Stakeholder Heatmap, Customer Insights — Latest, and my calendar. Produces a prioritized brief: what's at risk today, what I promised to do, what customers said overnight, what decisions need revisiting. Written to a dated file and ready when I wake up.

**Evening Debrief (6 PM weekdays)**
A write-enabled run. Reads: today's brief, Slack activity, calendar. Produces: a plan-vs-reality comparison, decision log for anything significant that happened, and a memory write-back that updates Open Loops, Risk Register, and Decision Ledger. The next morning's brief reflects these updates automatically.

**Weekly Radar (Saturday 3 AM)**
Synthesizes the week's patterns across all memory files. Produces customer insight rollups and surfaces strategic signals that only become visible across 5 days of data.

### Layer 3 — PM OS Memory

Persistent markdown files with stable IDs. Every scheduled run reads from and writes to these files, creating continuity across days.

| Memory file | Purpose | ID format |
|-------------|---------|-----------|
| Open Loops | Active commitments and follow-ups | `L-###` |
| Decision Ledger | Product decisions with rationale + revisit triggers | `D-###` |
| Risk Register | Active risks with ownership and mitigations | `R-###` |
| Stakeholder Heatmap | Trust-state and wait-state per stakeholder | `S-###` |
| Customer Themes | Recurring signals with evidence and weight | `T-###` |
| Customer Insights — Latest | Rolling 7-day meeting intelligence window | — |

Stable IDs mean the AI can cross-reference: a risk can link to the decision that created it, which links to the open loop tracking its resolution, which links to the customer theme that motivated it in the first place. This isn't just note-taking — it's a knowledge graph.

### Layer 4 — On-Demand Skills

Beyond scheduled runs, Claude has specialized workflows I can invoke on demand:

- **Write spec / PRD:** Structured question-by-question PRD builder that produces a spec with success criteria, measurement approach, and phase breakdown
- **Competitive brief:** Deep dive on a specific competitor or feature area, pulling from the Intel Log and live sources
- **Sprint planning:** Capacity-aware sprint plan with P0/P1/stretch breakdown
- **Stakeholder update:** Audience-tuned status update (exec brief, engineering detail, or customer-facing)
- **Synthesize research:** Turns interview notes, survey responses, or Slack threads into structured insight themes

---

## What a Day Looks Like

```
7:00 AM
  → Open Morning Brief (already generated, no prompting needed)
  → See today's P0/P1 priorities, overnight customer signals, open risks
  → 5 minutes to understand the day's context vs. 20+ minutes of manual review

9:30 AM
  → Customer call
  → Fireflies records and transcribes automatically

11:00 AM
  → Engineering sync reveals a dependency issue
  → Ask Claude: "Log a new decision — we're descoping [Feature X], reason is [Z]"
  → Claude writes to Decision Ledger, creates a Jira comment, drafts Slack update for review

2:00 PM
  → Need to brief a stakeholder on the change
  → Ask Claude: "Draft a stakeholder update on the [Feature X] timeline change for [Stakeholder A]"
  → Claude pulls context from Decision Ledger + Risk Register, drafts the message

6:00 PM
  → Evening Debrief auto-runs
  → Morning brief is already updated for tomorrow
```

---

## The Competitive Intelligence System

Separate from PM OS but integrated with it, a competitive intel pipeline runs automatically:

**Daily (7:30 AM weekdays):** A multi-agent orchestrator spawns sub-agents per competitor, each fetching Tier 1 sources (changelogs, blogs, job posts, pricing pages). RSS feeds are used where available. Results are merged, classified by category and confidence, deduplicated against a `last-run.json` file, and written to a dated output file and an append-only Intel Log with stable `CI-###` IDs.

**Weekly (Friday 8 PM):** A synthesis run reads the week's daily outputs, identifies cross-competitor patterns, surfaces strategic implications, and writes a weekly synthesis document.

When a competitive signal is strategically relevant, it's linked to PM OS entries — a risk, a decision under review, or a customer theme being validated.

---

## Technical Stack

| Component | Technology |
|-----------|-----------|
| AI | Claude (Anthropic) — Cowork desktop app |
| Scheduling | Cowork scheduled tasks (cron, IST timezone) |
| Tool connections | MCP (Model Context Protocol) |
| Memory layer | Markdown files with stable IDs, local workspace |
| Validation | Python script — checks schema integrity after every write |
| Multi-agent | Sub-agents for parallel competitive source fetching |
| Version control | Git (local, no secrets committed) |

---

## What This Has Changed

**Before:** I'd start most mornings reconstructing context — what did I say I'd do, what's at risk, what did customers say last week. This would take 20–30 minutes of email/Slack/Jira archaeology.

**After:** Context is reconstructed for me overnight. I open one file and I'm oriented.

**Before:** Competitive intel was something I'd try to do "when I had time" — which meant it happened sporadically and reactively.

**After:** Signals arrive daily. I read a 5-minute digest instead of doing 2 hours of research.

**Before:** Decisions and their rationale lived in my head, or scattered across Notion pages nobody read consistently.

**After:** Every significant decision is logged with rationale, alternatives considered, and a revisit trigger. The morning brief surfaces them when the trigger condition appears.

**The net effect:** More time on actual PM thinking, less on meta-work. And better institutional memory — not just for me, but for the AI that works with me.

---

## Explore the Samples

This showcase folder contains sanitized examples of every system component. No real company data, no identifying information — the structure and format are what matter.

- [PM OS samples →](./01-PM-OS/overview.md)
- [Connected Tools detail →](./02-Connected-Tools/connected-tools.md)
- [Competitive Intel samples →](./03-Competitive-Intel/overview.md)
