---
type: concept
title: G-Brain Nocturno — Access Policy
tags: [policy, access, security]
---

## Fuentes Autorizadas

### Google Drive
- **Leer:** Solo documentos con IDs explícitos en `brain/USER.md`, o encontrados por búsqueda de nombre exacto (Presupuesto CS, SteerCos)
- **Crear:** Solo documentos tipo "G-Brain — Sueños [fecha]" y "G-Brain Weekly Briefing"
- **Modificar:** Prohibido modificar documentos existentes (solo lectura)

### Slack
- **Leer:** Solo los 5 canales listados en `brain/USER.md`
- **Escribir:** Solo en #bdr_global (C03SHGED1FW) para la routine `friday-reminder`
- **Prohibido:** Enviar mensajes en canales de análisis (#revenue, #revenue-chile, #revenue-mexico, #revenue-peru)

### Web Search
- **Buscar:** Solo información pública sobre los 21 clientes listados en `brain/USER.md`
- **Fuentes prioritarias:** Df.cl, La Tercera Pulso, Bloomberg Línea, Emol Economía, El Financiero MX
- **Prohibido:** Acceder a fuentes que requieran autenticación

### Google Calendar
- **Leer:** Calendario de Tristan — calendar ID en `brain/USER.md`
- **Escribir:** Solo actualizar descripción del evento "Weekly Planning Review"
- **Prohibido:** Crear, eliminar o mover eventos

## Restricciones Editoriales

- NO incluir performance individual de personas
- NO incluir cambios de estructura organizacional
- NO fabricar datos sin fuente verificable de las tres fuentes autorizadas
- NO hacer inferencias sin evidencia de al menos 2 fuentes independientes

## Idempotencia

- `gbrain-gary-tan`: verificar si "G-Brain — Sueños [fecha]" ya existe antes de crear
- `weekly-planning`: verificar que el evento "Weekly Planning Review" existe antes de actualizar
- Si la operación ya fue ejecutada hoy: registrar timestamp y salir sin duplicar

## Modelo de Datos (Knowledge Model)

Todo output de largo plazo sigue el formato:
```
[VERDAD COMPILADA — reescribible]

---

[TIMELINE — append only, nunca editar entradas existentes]
- YYYY-MM-DD HH:MM: hecho con fuente
```

---

- 2026-04-18: Policy creada. G-Brain activado para Wherex / Tristan Riquelme.
