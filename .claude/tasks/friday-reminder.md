---
name: friday-reminder
type: deterministic
trigger: cron
resolver_entry: "send friday weekly relevantes reminder to bdr_global"
schedule: "0 9 * * 5"
timezone: America/Santiago
connectors:
  - slack
dependencies: []
models:
  fast: none
cost_per_run: "$0.00"
success_metrics:
  - message delivered to #bdr_global
  - correct channel confirmed (C03SHGED1FW)
---

Envía un mensaje al canal #bdr_global de Slack (ID: C03SHGED1FW) recordando
al equipo de Sales enviar sus relevantes de la semana antes del mediodía.

Mensaje exacto a enviar:

"🔔 Buenos días. Recordatorio: envío de relevantes de la semana
antes de las 12:00. Formato H/L por cuenta con next step concreto."

Confirma el timestamp de entrega al finalizar.
