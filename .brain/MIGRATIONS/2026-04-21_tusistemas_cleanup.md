# Migracion v1.3.0 — Limpieza de marca tusistemas
**App**: joshimitzu-autolavado (Control Autolavado)
**Familia**: Taller/Servicio
**Push automatico del orquestador**: 2026-04-21
**Aplicada al codigo app**: PENDIENTE ⚠️

---

## Referencia completa
Ver: `platform/base-app-template/docs/migrations/v1.3.0-tusistemas-cleanup.md`

> ⚠️ **LEER ESTE ARCHIVO ANTES DE CUALQUIER OTRO TRABAJO.**

---

## Resumen de lo que cambio en la plataforma

- Eliminacion total de la marca "tusistemas" de todos los archivos
- Salt de backup: "tusistemas-salt" → "joshimitzu-salt"
- appId: "com.tusistemas.*" → "com.joshimitzu.*"
- Dominio: sin referencias a dominio externo (pendiente definicion)

---

## Tareas de reconciliacion

- [ ] **Tarea 1** — Verificar que no existen strings "tusistemas" en el repo
  ```bash
  grep -r "tusistemas" . --include="*.ts" --include="*.tsx" --include="*.json" --include="*.md" --exclude-dir=node_modules
  ```
  Si no hay resultados: marcar como completada automaticamente.

- [ ] **Tarea 2** — Verificar APP_NAME/APP_COLOR en .env.local
  ```
  APP_SLUG=autolavado
  APP_NAME="Control Autolavado"
  APP_COLOR=#1d4ed8
  ```

- [ ] **Tarea 3** — Commit de verificacion si se encontraron strings a corregir

---

## Checklist de ejecucion

- [ ] Tarea 1 completada — sin strings "tusistemas" encontrados
- [ ] Tarea 2 completada — .env.local verificado
- [ ] Tarea 3 — solo si hubo correcciones: commit SHA: ____

---

## Autorizacion del usuario
Requerida antes de ejecutar: **"si, autorizo"**
Autorizada: ☐ (pendiente)
