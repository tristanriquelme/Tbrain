---
name: wherex-weekly-synthesis
type: skill
description: >
  Synthesizes weekly Slack updates from Pre-Sales, Sales, CS, and RevOps teams into a
  polished executive leadership document for Wherex. Use this skill whenever Tristan shares
  raw Slack inputs from his teams and asks for a weekly update, relevantes, synthesis,
  resumen semanal, or leadership doc. Also triggers when inputs arrive incrementally
  (one team at a time) and Tristan says "arrancamos" or confirms all inputs are in.
  This skill handles Spanish and English inputs interchangeably.
used_by:
  - friday-synthesis
---

# Wherex Weekly Synthesis Skill

## Purpose
Transform raw Slack updates from 4 teams (Pre-Sales, Sales, CS, RevOps) into a clean,
fact-only executive leadership document. Remove all fluff, sentiment, and backstory.
Surface only: named account + concrete action + metric/number + specific blocker + risk signal.

---

## Output Structure

```
[Date]

Kudos 😁
- [copy kudos as-is]

Revenue [TR]

  Pre-Sales
    Highlights
    Lowlights

  Sales
    Highlights
      *Chile* (geo sub-header if >5 bullets)
      *México*
      *Perú*
      *Colombia*
    Lowlights
      (same geo sub-headers if >5 bullets)

  RevOps
    Highlights
    Lowlights

Retención / CS [TR]

  Onboarding
    Highlights / Lowlights (geo sub-headers if >5 bullets)

  Cross-sell
    Highlights / Lowlights (geo sub-headers if >5 bullets)

  Engagement
    Highlights / Lowlights (geo sub-headers if >5 bullets)

  Match / Operaciones (only if there are material items)
    Highlights / Lowlights

Métricas pendientes de corrección [TR] (only if metrics need correction)

⚠️ Para revisión manual [TR]
  Sales
  CS
  (other sections as needed)
```

---

## Transformation Rules

### Ownership & Tags
- `[TR]` appears once at the section header level: **Revenue [TR]** and **Retención / CS [TR]**
- Do NOT repeat `[TR]` on individual bullets
- Original author initials are used internally only to identify source — never appear in the leadership doc body
- Kudos section: copy as-is, no tag needed

### Geography
- Countries are inline prefixes when bullets are few: `- CL Caserones: contrato firmado.`
- When a section has >5 bullets, group with italic geo sub-headers: `*Chile*`, `*México*`, `*Perú*`, `*Colombia*`
- Drop geo prefix from individual bullets once under a geo sub-header

### Language & Tone

**Strip:**
- All sentiment adjectives: "muy buena", "excelente", "fuerte", "promisorio", "increíble"
- Intentions without committed date: "buscaremos", "esperamos", "tenemos intención de"
- Contextual backstory and internal justifications
- Effort without outcome: "hemos intentado varias veces" → only keep the concrete status
- Ambiguous quantities: "varios", "muchos", "bastante", "harta", "mucho interés", "several", "many", "a lot", "very much" → replace with exact number if available; cut entirely if no number exists. Never carry vague quantities into the output.

**Keep:**
- Named account + concrete action
- Specific numbers and metrics
- Named blockers with cause
- Risk signals (churn, no shows, budget cuts, key contact departures)
- Deal size, GMV, adjudication amounts

**Transform:**
- Passive to active + concrete: "hubo avances" → specific action taken
- Hedged language stripped: "parecería que", "posiblemente" → state as fact or move to postscript

### Metrics & Numbers
- Always keep: PCR, GMV, GTV, COM, adjudication amounts, USD/MXN/PEN amounts, deal sizes, counts
- When a number is missing but should exist, add: `Pendiente [dato] — solicitar a [owner]`
- **Quantification rule**: Any time the report states that a number was obtained, estimated, levantado, cuantificado, or shared by the client — gasto licitable, monto transable, recurrentes, presupuesto, ahorro, adjudicación, or any other metric explicitly characterized as known or obtained — the actual number must appear in the bullet. If not provided, add: `Pendiente monto — solicitar a [owner handle]`
- **Savings rule**: Only when the report explicitly mentions "ahorros", "savings", or a direct cost comparison — add: `Pendiente monto de ahorro — solicitar a [owner handle]` if the amount is not provided. Do NOT request savings for adjudications where no savings are mentioned.
- Metrics reported for wrong period: flag in **Métricas pendientes de corrección** section, include the numbers with period label, tag the owner's Slack handle

### Postscript Criteria
Move to postscript — NEVER silently drop — when:
- No concrete next step with a date
- Ambiguous status (loss? pause? long pipeline?)
- Impact on ARR not clear
- Deal is clearly long-term with no near-term milestone
- Internal conversation not a formal report
- Item needs Tristan's judgment before classifying

**Duplication rule**: Any bullet in the body that contains a pending action, data request, or escalation (e.g. "Pendiente monto", "Escalar a Producto", "Confirmar con X") must ALSO appear in the postscript. The body is for leadership consumption; the postscript is TR's working checklist. They are not mutually exclusive.

---

## Postscript Format

Group by section (Sales / CS / etc.) for easy Slack posting per channel.

```
**⚠️ Para revisión manual [TR]**

**Sales**

[INITIALS] GEO Account
"Texto original literal del Slack" >> [TR] Acción recomendada concreta. @SlackHandle
```

Each item must have:
1. Section header (Sales / CS / RevOps / Pre-Sales)
2. [INITIALS] GEO Account label
3. Exact original quote in italics
4. >> [TR] recommended action
5. @SlackHandle of the owner

---

## Slack Handle Map

| Initials | Name | Slack Handle |
|---|---|---|
| AC | Agustin Corssen | @Agustin Corssen |
| AD | Agustín Donoso | @Agustín Donoso |
| AYS | Catalina Araya Tejada | @Catalina Araya Tejada |
| FC | Fiorella Castellano | @Fiorella Castellano |
| FL | Felipe Lira | @Felipe Lira |
| FP | Francisco Puente | @Francisco Puente |
| SG | Sofía Garcés | @Sofía Garcés |
| IR | Isa Rincón | @IsaRincón |
| JL | Jorge López | @Jorge López |
| JTM | José Tomás Márquez | @José Tomás Márquez Fuenzalida |
| LL | Lucas Lorenzini | @Lucas Lorenzini |
| LFZ | Luis Felipe Zanoni | @Luis Felipe Zanoni |
| MA | Matías Almeida | @Matías Almeida |
| MCM | María Camila Márquez | @María Camila Márquez |
| MV | Mauricio Villegas | @Mauricio Villegas |
| PM | Pepe Macías | @José Norberto Macías Hernández |
| PN | Paulo Nuñez Del Prado | @Paulo Nuñez Del Prado |
| SL | Sergio Leguizamon | @Sergio Leguizamon |
| TRub | Tomás Rubinstein | @Tomás Rubinstein |
| TR | Tristan Riquelme | @Tristan Riquelme |

---

## Section-Specific Rules

### Pre-Sales
- Keep PCR metrics always: actual vs presupuesto, week over week
- SDR hiring: keep only concrete milestones (hired, start date, PCR target) — strip enthusiasm
- Pipeline agencies or initiatives "en evaluación": move to postscript unless decision made

### Sales
- Geo sub-headers when >5 bullets per H/L block
- First meetings: keep only if next step is concrete (demo scheduled, proposal date set)
- "En evaluación" or "revisando internamente": keep in body only if next step has a date; otherwise postscript
- Lost deals: one line — reason and disposition (mandada a pérdida / reagendando)
- No shows: report as ratio (X/Y reuniones) and flag if recurring pattern

### RevOps
- Keep all technical milestones with go-live dates
- Issues without root cause diagnosed: flag as "pendiente diagnóstico"

### CS — Onboarding
- Milestones only: first session, full cycle complete, first process published, integration started
- Blocked onboardings: state blocker explicitly, flag if >2 weeks without resolution

### CS — Cross-sell
- Keep: product confirmed, contract in process, demo scheduled
- Strip: "interés general" without next step — move to postscript

### CS — Engagement
- Licitaciones relevantes: always include GMV/adjudication amount
- Savings: only when explicitly mentioned by the reporter — request amount if not provided
- Churn signals: always surface explicitly with "Riesgo de churn activo"
- Key contact departures: always flag with commission/ARR impact if known

### CS — Match / Operaciones
- Include only when there is material operational risk to a client relationship
- Strip routine operational updates with no client impact

---

## Edge Cases

- **Duplicate reports**: Always use latest timestamp version
- **Internal chat mistakenly pasted**: Move to postscript, do not include in body
- **Metrics for wrong period**: Flag in dedicated correction section, do not silently use
- **"POC pagada"**: Always confirm with owner whether ARR is associated before including in body
- **Accounts belonging to known groups**: Note group relationship inline (e.g., "Pertenece a Grupo DC, ya cliente")
- **Ariba / competitor mentions**: Always note inline — relevant for positioning context
