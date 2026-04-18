---
type: concept
title: G-Brain Nocturno — Resolver
tags: [resolver, routing, skills]
---

## Skill Routing

| Trigger | Skill | Type | Description |
|---------|-------|------|-------------|
| `cron: 30 23 * * *` (America/Santiago) | `gbrain-gary-tan` | judgment | Análisis nocturno — genera Sueños en Drive |
| `cron: 0 9 * * 5` (America/Santiago) | `friday-reminder` | deterministic | Recordatorio semanal relevantes a Sales, Pre-Sales/RevOps y CS |
| `cron: 0 17 * * 5` (America/Santiago) | `friday-synthesis` | judgment | Síntesis de relevantes semanales → Relevantes SLT en Drive |
| `cron: 0 22 * * 0` (America/Santiago) | `weekly-planning` | judgment | Briefing semanal + actualiza evento calendario lunes |

## Dependency Graph

```
gbrain-gary-tan (judgment)
├── signal-detector     — extrae entidades de Drive + Slack
├── brain-ops           — compiled truth map; brain-first antes de web search
├── enrich              — tiered enrich (Tier 1/2/3) para clientes con noticias
├── cross-modal-review  — quality gate: valida patrones, hipótesis, fuentes
└── reports             — guarda Sueños con header timestamped en Drive

weekly-planning (judgment)
├── brain-ops           — lee docs Drive, construye contexto
├── daily-task-prep     — lookahead calendario con contexto de cuentas
└── reports             — actualiza descripción evento Calendar con briefing

friday-reminder (deterministic)
└── (ninguna — mensaje directo a Slack, sin brain lookup)

friday-synthesis (judgment)
├── brain-ops           — carga contexto de cuentas antes de leer Slack
└── reports             — append Knowledge Model en Relevantes SLT (Drive)
```

## MECE Check

- Cada trigger cron apunta a exactamente una skill
- Sin triggers solapados
- Sin skills huérfanas
- Routing deterministic vs. judgment correcto:
  - `friday-reminder`: mismo input → mismo output → deterministic ✓
  - `friday-synthesis`: síntesis de mensajes Slack variables → judgment ✓
  - `gbrain-gary-tan`: requiere síntesis de fuentes variables → judgment ✓
  - `weekly-planning`: requiere síntesis de docs + calendario variable → judgment ✓

## Convenciones de Skill

Cada archivo en `.claude/tasks/` sigue el estándar SKILL.md:
- Frontmatter: `name`, `type`, `trigger`, `resolver_entry`, `schedule`, `timezone`, `connectors`, `dependencies`, `models`, `cost_per_run`, `success_metrics`
- Cuerpo: prompt completo con pasos numerados
- Idioma del prompt: español

---

- 2026-04-18: Resolver creado para G-Brain Nocturno (3 skills, 0 conflictos).
