# PM OS — Overview

## What it is

PM OS is a persistent memory and accountability system for product managers, powered by Claude. It runs automatically every weekday and maintains a structured knowledge base that grows over time.

Think of it as a second brain that never forgets what you committed to, why you made a decision, or what your customers are worried about.

---

## How it works

### Four scheduled runs

| Run | When | What it does | Writes? |
|-----|------|-------------|---------|
| **Fireflies Harvest** | Nightly, 1 AM | Pulls meeting transcripts from Fireflies, extracts customer signals, updates `Customer Insights — Latest.md` | ✅ Yes |
| **Morning Brief** | 6 AM weekdays | Reads all memory files + latest customer insights. Produces a prioritized brief: risks, commitments, blockers for the day | ❌ Read-only |
| **Evening Debrief** | 6 PM weekdays | Captures what happened, compares plan vs. reality, writes back to Open Loops, Risk Register, Decision Ledger | ✅ Yes |
| **Weekly Radar** | Saturday, 3 AM | Synthesizes the week's patterns, updates Customer Insights weekly rollups, surfaces strategic signals | ✅ Yes |

### Memory files

Each file uses stable IDs so AI can cross-reference across runs:

| File | Purpose | ID format |
|------|---------|-----------|
| `Open Loops.md` | Active commitments and follow-ups | `L-###` |
| `Decision Ledger.md` | Product decisions with rationale + revisit triggers | `D-###` |
| `Risk Register.md` | Active risks with ownership + mitigations | `R-###` |
| `Stakeholder Heatmap.md` | Stakeholder trust-state and wait-state tracking | `S-###` |
| `Customer Themes.md` | Recurring customer signals with evidence | `T-###` |
| `Customer Insights — Latest.md` | Rolling 7-day window of meeting summaries | — |

---

## What a typical day looks like

```
7:00 AM  →  Read Morning Brief (auto-generated, already waiting)
             — What's at risk today
             — What I committed to yesterday
             — Overnight customer signals from meetings

[... work happens ...]

6:00 PM  →  Evening Debrief triggers
             — Did I do what I said I'd do?
             — What changed? What's now blocked?
             — System writes back: closes loops, updates risks, logs decisions

Next morning: Brief already knows about yesterday's debrief
```

---

## Sample artifacts

- [Sample Morning Brief →](./sample-morning-brief.md)
- [Sample Evening Debrief →](./sample-evening-debrief.md)
- [Open Loops (sample) →](./sample-memory-files/open-loops.md)
- [Decision Ledger (sample) →](./sample-memory-files/decision-ledger.md)
- [Risk Register (sample) →](./sample-memory-files/risk-register.md)
