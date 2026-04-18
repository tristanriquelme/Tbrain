# G-Brain Nocturno — Tbrain Automation Repository

## Purpose

Automated intelligence-gathering and synthesis system for Tristan Riquelme, CRO of Wherex.
Runs nightly and weekly routines via Claude Code scheduled tasks to produce strategic briefings
called "Sueños" from Google Drive, Slack, and public web sources.

Architecture based on [GBrain](https://github.com/garrytan/gbrain) by Garry Tan.

## Routines

| File | Name | Schedule (Chile) | Connectors |
|------|------|-----------------|------------|
| `gbrain-gary-tan.md` | gbrain-gary-tan | Nightly 23:30 | Google Drive, Slack, Web |
| `friday-reminder.md` | friday-reminder | Fridays 09:00 | Slack |
| `friday-synthesis.md` | friday-synthesis | Fridays 17:00 | Slack, Google Drive |
| `weekly-planning.md` | weekly-planning | Sundays 22:00 | Google Drive, Google Calendar |

All schedules use `timezone: America/Santiago` (UTC-4 standard / UTC-3 summer, DST-aware).

## Required Connectors

Authorize at: https://claude.ai/settings/connectors

- **Google Drive** — reads strategic docs, creates Sueños output doc
- **Slack** — reads revenue channels, posts Friday reminder
- **Web Search** — searches news for 21 priority clients
- **Google Calendar** — reads and updates Weekly Planning Review event

## Repository Structure

```
Tbrain/
├── CLAUDE.md                    ← this file
├── brain/
│   ├── SOUL.md                  ← G-Brain identity and mission
│   ├── USER.md                  ← Tristan's profile, doc IDs, channel IDs, clients
│   └── ACCESS_POLICY.md         ← Data access rules and editorial restrictions
├── skills/
│   └── RESOLVER.md              ← Skill routing table and dependency graph
└── .claude/
    ├── settings.json            ← Connector permissions
    └── tasks/
        ├── gbrain-gary-tan.md   ← Main nightly routine
        ├── friday-reminder.md   ← Friday 09:00 Slack reminder (Sales, Pre-Sales, CS)
        ├── friday-synthesis.md  ← Friday 17:00 synthesis → Relevantes SLT in Drive
        └── weekly-planning.md   ← Sunday weekly planning
```

## Knowledge Model (GBrain Pattern)

All output documents follow the GBrain Knowledge Model:

```markdown
[COMPILED TRUTH — current best understanding, rewritable]

---

[TIMELINE — append-only evidence trail]
- YYYY-MM-DD HH:MM: dated evidence with source
```

**Above separator:** Synthesized analysis (patterns, hypotheses, briefings) — rewritten when new evidence changes the picture.
**Below separator:** Raw evidence with timestamps and sources — never edited, only appended.

## GBrain Concepts Applied

| Concept | Applied in |
|---------|-----------|
| Signal-Detector | `gbrain-gary-tan` — entity extraction from Drive + Slack on every run |
| Brain-First Lookup | `gbrain-gary-tan` HILO 3 — checks compiled truth before web search |
| Tiered Enrich (Tier 1/2/3) | `gbrain-gary-tan` HILO 3 — structured fact extraction per client |
| Cross-Modal Review | `gbrain-gary-tan` PASO 2 — quality gate before output |
| Cron Idempotency | `gbrain-gary-tan` PASO 0 — checks for existing doc before creating |
| Wherex Weekly Synthesis | `friday-synthesis` — editorial transformation rules, geo breakdown, postscript |
| Knowledge Model | Output format for Sueños and weekly briefings |
| Reports Format | Timestamped headers with keyword routing on all saved docs |
| SKILL.md Frontmatter | All task files — `type`, `trigger`, `dependencies`, `models`, `cost_per_run`, `success_metrics` |
| Brain-Ops | `weekly-planning` — brain-first context load before generating briefing |
| Daily-Task-Prep | `weekly-planning` — calendar lookahead with account context |
| Soul Audit | `brain/SOUL.md`, `brain/USER.md`, `brain/ACCESS_POLICY.md` |
| RESOLVER | `skills/RESOLVER.md` — skill routing, MECE check, dependency graph |

## Google Drive Documents

| Doc name | ID | Used by |
|----------|----|---------|
| G-Brain — Estado Activo (master) | `1TLgbZgdehDlcHH4pb4wRyVn6Hf7XgZlv2KIT2L2Bjak` | gbrain-gary-tan, weekly-planning |
| Relevantes CS 2026 | `11Ux3z17eXvtOG0kRJs12_rG0KzWxrX8uIaGoinXxJeA` | gbrain-gary-tan, weekly-planning |
| Relevantes SLT 2026 | `1q-kNUlgtq7KAaI2TIUD9n7kxXBTiy4F0O6qkplrkylE` | gbrain-gary-tan, weekly-planning, friday-synthesis |
| Narrativa Retención | `111a2K_NcQBk6BPOdgXHE_B5wVOJtk69lz_s53p5O1us` | gbrain-gary-tan, weekly-planning |
| Narrativa CX | `1MgTtseOGuyVwnB-M5AnvT7iaSilMHEZQV6If0n3APxI` | gbrain-gary-tan, weekly-planning |
| Narrativa Marketplace | `1QvytEsb3iIyl0i9QlQXmR83u7E5rWFSc7lJMmWRhaRo` | gbrain-gary-tan, weekly-planning |
| Presupuesto CS | *(search by name)* | weekly-planning |
| SteerCos | *(search by name)* | weekly-planning |

## Slack Channels

| Channel | ID | Monitored by |
|---------|----|-------------|
| #revenue | `C087V8PDSTB` | gbrain-gary-tan |
| #bdr_global (Sales) | `C03SHGED1FW` | gbrain-gary-tan, friday-reminder, friday-synthesis |
| Pre-Sales / RevOps | `C02MW42D8F4` | friday-reminder, friday-synthesis |
| Customer Success | `C06GB14B5PC` | friday-reminder, friday-synthesis |
| #revenue-chile | `C0ADH2XTQU8` | gbrain-gary-tan |
| #revenue-mexico | `G01PDDB259A` | gbrain-gary-tan |
| #revenue-peru | `C0A0S1315HT` | gbrain-gary-tan |
| SLT | `C01QPB0B371` | gbrain-gary-tan |

## Google Calendar

- **Weekly Planning Review event** — Monday 08:00 AM Chile time
- Calendar ID: `i66ia4t951r9pp9l6tavgub8vc`
- Updated by: weekly-planning routine
