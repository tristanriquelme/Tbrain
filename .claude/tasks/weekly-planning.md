---
name: weekly-planning
description: Briefing semanal dominical — lee Drive y calendario, genera resumen y actualiza evento del lunes
schedule: "0 22 * * 0"
timezone: America/Santiago
connectors:
  - google-drive
  - google-calendar
---

Lee el calendario de Tristan para la semana siguiente.
Lee los docs Drive modificados en los últimos 7 días:

- G-Brain — Estado Activo (ID: 1TLgbZgdehDlcHH4pb4wRyVn6Hf7XgZlv2KIT2L2Bjak)
- Relevantes CS 2026 (ID: 11Ux3z17eXvtOG0kRJs12_rG0KzWxrX8uIaGoinXxJeA)
- Relevantes SLT 2026 (ID: 1q-kNUlgtq7KAaI2TIUD9n7kxXBTiy4F0O6qkplrkylE)
- Narrativa Retención (ID: 111a2K_NcQBk6BPOdgXHE_B5wVOJtk69lz_s53p5O1us)
- Presupuesto CS (buscar por nombre en Drive)
- SteerCos (buscar por nombre en Drive)

Genera un briefing de la semana con este formato:

---
BRIEFING SEMANAL — Semana del [FECHA_LUNES] al [FECHA_VIERNES]

PRIORIDADES
[3-5 prioridades concretas derivadas de los docs]

COMPROMISOS CON FECHA
[Lista de compromisos con deadline esta semana]

CUENTAS A MONITOREAR
[Cuentas mencionadas en relevantes con movimiento activo]

FOCO ESTRATÉGICO
[1 párrafo: qué debe avanzar obligatoriamente esta semana]
---

Actualiza la descripción del evento "Weekly Planning Review" del lunes 8:00 AM
(Calendar ID: i66ia4t951r9pp9l6tavgub8vc) con el briefing generado.
