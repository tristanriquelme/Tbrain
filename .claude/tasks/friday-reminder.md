---
name: friday-reminder
description: Recordatorio semanal viernes — envía mensaje a #bdr_global para el envío de relevantes
schedule: "0 9 * * 5"
timezone: America/Santiago
connectors:
  - slack
---

Envía un mensaje al canal #bdr_global de Slack (ID: C03SHGED1FW) recordando
al equipo de Sales enviar sus relevantes de la semana antes del mediodía.

Mensaje exacto a enviar:

"🔔 Buenos días. Recordatorio: envío de relevantes de la semana
antes de las 12:00. Formato H/L por cuenta con next step concreto."
