# G-Brain Nocturno — Tbrain Automation Repository

## Purpose

Automated intelligence-gathering and synthesis system for Tristan Riquelme, CRO of Wherex.
Runs nightly and weekly routines via Claude Code scheduled tasks to produce strategic briefings
called "Sueños" from Google Drive, Slack, and public web sources.

## Routines

| File | Name | Schedule (Chile) | Connectors |
|------|------|-----------------|------------|
| `gbrain-gary-tan.md` | gbrain-gary-tan | Nightly 23:30 | Google Drive, Slack, Web |
| `friday-reminder.md` | friday-reminder | Fridays 09:00 | Slack |
| `weekly-planning.md` | weekly-planning | Sundays 22:00 | Google Drive, Google Calendar |

All schedules use `timezone: America/Santiago` (UTC-4 standard / UTC-3 summer, DST-aware).

## Required Connectors

Authorize at: https://claude.ai/settings/connectors

- **Google Drive** — reads strategic docs, creates Sueños output doc
- **Slack** — reads revenue channels, posts Friday reminder
- **Web Search** — searches news for 21 priority clients
- **Google Calendar** — reads and updates Weekly Planning Review event

## Google Drive Documents

| Doc name | ID | Used by |
|----------|----|---------|
| G-Brain — Estado Activo (master) | `1TLgbZgdehDlcHH4pb4wRyVn6Hf7XgZlv2KIT2L2Bjak` | gbrain-gary-tan, weekly-planning |
| Relevantes CS 2026 | `11Ux3z17eXvtOG0kRJs12_rG0KzWxrX8uIaGoinXxJeA` | gbrain-gary-tan, weekly-planning |
| Relevantes SLT 2026 | `1q-kNUlgtq7KAaI2TIUD9n7kxXBTiy4F0O6qkplrkylE` | gbrain-gary-tan, weekly-planning |
| Narrativa Retención | `111a2K_NcQBk6BPOdgXHE_B5wVOJtk69lz_s53p5O1us` | gbrain-gary-tan, weekly-planning |
| Presupuesto CS | *(search by name)* | weekly-planning |
| SteerCos | *(search by name)* | weekly-planning |

## Slack Channels

| Channel | ID | Monitored by |
|---------|----|-------------|
| #revenue | `C087V8PDSTB` | gbrain-gary-tan |
| #bdr_global | `C03SHGED1FW` | gbrain-gary-tan, friday-reminder |
| #revenue-chile | `C0ADH2XTQU8` | gbrain-gary-tan |
| #revenue-mexico | `G01PDDB259A` | gbrain-gary-tan |
| #revenue-peru | `C0A0S1315HT` | gbrain-gary-tan |

## Google Calendar

- **Weekly Planning Review event** — Monday 08:00 AM Chile time
- Calendar ID: `i66ia4t951r9pp9l6tavgub8vc`
- Updated by: weekly-planning routine
