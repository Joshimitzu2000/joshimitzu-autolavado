---
app_slug: autolavado
family: taller
brand_color: "#1d4ed8"
platform_version_locked: "1.3.0"
current_phase: "not_started"
current_branch: "main"
last_updated: "2026-05-13T16:13:57.018Z"
last_session_by: "orchestrator"
---

# STATE — joshimitzu-autolavado

> **Para cualquier IA:** Lee este archivo ANTES de proponer trabajo.
> Actualízalo al cerrar la sesión (ver PROTOCOLO DE SESIÓN en INSTRUCCIONES.md).

---

## Identidad invariante (NO modificar)

- **Nombre comercial:** Control Autolavado
- **Familia:** Taller/Servicio
- **Color de marca:** #1d4ed8 — INMUTABLE
- **appId:** com.joshimitzu.autolavado
- **Repo:** github.com/Joshimitzu2000/joshimitzu-autolavado

---

## Fase actual

**not_started** — App creada. Infraestructura de plataforma lista (v1.3.0).
Pendiente: absorber migración v1.3.0, luego iniciar Fase 1 (dominio + schema).

⚠️ **LEER `.brain/MIGRATIONS/` ANTES DE TRABAJAR.**

---

## Módulos completados

_(ninguno — app sin desarrollo propio todavía)_

---

## En curso

_(ninguno)_

---

## Próximo paso concreto

1. Leer `.brain/MIGRATIONS/2026-04-21_tusistemas_cleanup.md` — verificar migración v1.3.0
2. Grep en repo: confirmar que no hay strings "tusistemas"
3. Crear `.env.local` con APP_SLUG=autolavado, APP_COLOR=#1d4ed8
4. Definir modelos de dominio específicos para Control Autolavado
5. Implementar Fase 1 según INSTRUCCIONES.md

---

## Decisiones arquitectónicas tomadas

_(ninguna — pendiente de primera sesión de desarrollo)_

---

## Desviaciones intencionales de base-app-template

_(ninguna todavía)_

---

## Migraciones pendientes

- **v1.3.0-tusistemas-cleanup** — verificar que no quedan strings "tusistemas" en el repo
  → ver `.brain/MIGRATIONS/2026-04-21_tusistemas_cleanup.md`

---

## Migraciones absorbidas

- v1.0.0 (initial) — creación desde template
- v1.1.0 (accessibility) — accesibilidad + contraste
- v1.2.0 (auth-dual) — sistema auth dual instalado desde base-app-template
