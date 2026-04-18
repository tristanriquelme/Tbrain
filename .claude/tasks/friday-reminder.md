---
name: friday-reminder
type: deterministic
trigger: cron
resolver_entry: "send friday weekly relevantes reminder to all revenue teams"
schedule: "0 9 * * 5"
timezone: America/Santiago
connectors:
  - slack
dependencies: []
models:
  fast: none
cost_per_run: "$0.00"
success_metrics:
  - mensaje entregado en #bdr_global (C03SHGED1FW)
  - mensaje entregado en canal Pre-Sales / RevOps (C02MW42D8F4)
  - mensaje entregado en canal Customer Success (C06GB14B5PC)
---

Envía un recordatorio de relevantes semanales a los equipos de revenue.
Envía **3 mensajes separados**, uno por canal, con el texto adaptado a cada equipo.

---

**Canal Sales — #bdr_global (`C03SHGED1FW`)**

"🔔 Buenos días equipo Sales. Recordatorio: envío de relevantes de la semana
antes de las 12:00. Formato H/L por cuenta con next step concreto."

---

**Canal Demand Gen / SDRs (`C02MW42D8F4`)**

"🔔 Buenos días equipo Demand Gen. Recordatorio: envío de métricas de la semana
antes de las 12:00. Incluir: reuniones calificadas generadas, cuentas trabajadas
en outbound, secuencias activas y tasa de respuesta. Si hubo bloqueo en alguna
cuenta o segmento, menciónalo."

---

**Canal Customer Success (`C06GB14B5PC`)**

"🔔 Buenos días equipo Customer Success. Recordatorio: envío de relevantes
de la semana antes de las 12:00. Formato H/L por cuenta con next step concreto."

---

Confirma el timestamp de entrega de los 3 mensajes al finalizar.
