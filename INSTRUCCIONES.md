# INSTRUCCIONES -- Control Autolavado
# Joshimitzu Software -- joshimitzu.com
#
# Archivo universal de instrucciones por app.
# Cualquier IDE o IA debe leer este archivo al iniciar y configurarse.

---

## PASO 1 -- AUTO-CONFIGURACION (ejecutar al abrir este repo)

Lee este archivo y crea o actualiza tu archivo nativo de instrucciones:

  Claude Code   -> CLAUDE.md (en la raiz del repo)
  Cursor        -> .cursorrules
  Windsurf      -> .windsurfrules
  GitHub Copilot-> .github/copilot-instructions.md
  Gemini        -> tu formato nativo de instrucciones
  Otro IDE      -> el archivo que tu herramienta lee automaticamente al iniciar

Copia el contenido completo de este archivo a ese archivo nativo.
Si el archivo ya existe, reemplaza su contenido.

---

## IDENTIDAD DE LA APP

  Nombre       : Control Autolavado
  Repo         : joshimitzu-autolavado
  GitHub       : https://github.com/Joshimitzu2000/joshimitzu-autolavado
  Color marca  : #1d4ed8
  appId        : com.joshimitzu.autolavado
  Familia      : Taller/Servicio
  Desarrollador: Joshimitzu Software -- joshimitzu.com

---

## REGLAS CRITICAS (no negociables)

  1. JAMAS push directo a main -- siempre via PR
  2. NO modificar DevBadge, DashboardShell, DashboardSidebar
  3. Color fijo: --brand-color: #1d4ed8
  4. appId fijo: com.joshimitzu.autolavado
  5. NO instalar dependencias sin justificarlas en el PR
  6. NO escribir codigo sin autorizacion de Joshua
  7. La autorizacion de Joshua es el mensaje exacto: 'si, autorizo'
  8. Todo desarrollo espera aprobacion -- investigacion primero

---

## PROTOCOLO DE SESION (obligatorio al abrir este repo)

  Cualquier IA que abra este repo debe ejecutar estos pasos ANTES de escribir codigo:

  Paso 1 -- Leer contexto en este orden exacto
    1. INSTRUCCIONES.md (este archivo)  -- reglas y identidad de la plataforma
    2. .brain/STATE.md                  -- estado actual de esta app especifica
    3. .brain/MIGRATIONS/               -- migraciones pendientes (ejecutar PRIMERO)
    4. .brain/CHANGELOG.md              -- historial de sesiones previas

  Paso 2 -- Reportar al usuario antes de cualquier accion
    Antes de proponer trabajo, reportar:
    - Que app es: nombre, familia, color, fase actual segun STATE.md
    - Que migraciones pendientes hay (si las hay, van ANTES que cualquier otra cosa)
    - Cual es el proximo paso segun STATE.md
    - La entrada mas reciente del CHANGELOG
    - Cualquier inconsistencia detectada (ej: archivo que STATE dice existir pero no existe)

  Paso 3 -- Solicitar autorizacion
    Jamas ejecutar cambios sin la frase exacta: 'si, autorizo'
    Sin esa frase, solo leer, analizar y reportar.

  Paso 4 -- Trabajar linealmente
    - Un modulo / tarea a la vez -- no abrir frentes paralelos
    - Commits atomicos: un proposito por commit
    - Si surge trabajo fuera del modulo actual: anotarlo en STATE.md
      seccion 'Proximas ideas' -- NO ejecutarlo en la misma sesion

  Paso 5 -- Al cerrar la sesion, SIEMPRE actualizar STATE.md
    - Mover tareas completadas a 'Modulos completados' con fecha
    - Actualizar 'Proximo paso concreto'
    - Agregar entrada a .brain/CHANGELOG.md con resumen de la sesion
    - Bumpear last_updated en front-matter de STATE.md
    - Commit: 'chore(state): update STATE after session'

---

## STACK TECNOLOGICO

  Next.js 15 + React 19 + TypeScript + Tailwind v4
  Prisma + NextAuth v5 + Zod + Electron

---

## PLATAFORMA JOSHIMITZU SOFTWARE

### Modelo de Negocio

  App local Electron (.exe) -- funciona 100% OFFLINE
  Pago unico (NO suscripcion) -- el cliente compra el programa una sola vez
  Premium Cloud opcional -- gestionado por Joshimitzu, el cliente no toca servidores

  Tiers de precio:
    Local (pago unico) : ~599 MXN  -- app completa offline, 1 equipo
    Premium Basic      : 99 MXN/mes -- + landing page + portal clientes + email
    Premium Pro        : 199 MXN/mes -- + dashboard remoto + backups en nube

  CRITICO para el IDE:
    - Features CORE del negocio van en el tier local (pago unico)
    - Features que requieren internet constante van en Premium Basic o Pro
    - NUNCA disenar features core que requieran conexion constante
    - NO usar PostgreSQL, MongoDB ni BD cloud -- SQLite cifrada local siempre
    - NO implementar SaaS ni per-seat pricing -- es pago unico por instalacion

### Los 6 Pilares Obligatorios

  El template base ya incluye la implementacion base de cada pilar.
  El IDE debe extender, NO reimplementar.

  Pilar 1 -- Licenciamiento JWT+RSA-256
    Activacion online obligatoria (una sola vez)
    Hardware fingerprint: 1 licencia = 1 equipo activo
    Validacion offline con clave publica RSA embebida
    -> Extender src/lib/license/ del template

  Pilar 2 -- Anti-piracy 7 capas
    BD cifrada: clave = SHA-256(licencia_jwt + hardware_fingerprint)
    Integrity check SHA-256 por archivo critico al arrancar
    Ofuscacion de frontend en builds de produccion
    -> El template incluye la base -- no tocar

  Pilar 3 -- Arquitectura Local-First
    SQLite cifrada como BD local
    App funciona sin internet despues de la activacion inicial
    Sincronizacion con servidor solo en tier Premium
    -> Extender prisma/schema.prisma con los modelos de negocio del dominio

  Pilar 4 -- Backup .appbak
    Archivo ZIP renombrado: datos + config + uploads + manifest.json
    NUNCA incluir licencia ni hardware fingerprint en el backup
    Boton 'Crear Respaldo' en panel admin -- OBLIGATORIO implementar
    -> Extender src/lib/backup/ del template

  Pilar 5 -- SemVer + OTA updates
    Patch/Minor = gratis y automaticos; Major = puede ser de pago
    Notificacion al usuario al iniciar si hay nueva version
    -> El template incluye src/lib/updater/ -- no reimplementar

  Pilar 6 -- Setup Wizard (PASO 4 ES TU RESPONSABILIDAD)
    Pasos 1-3 ya estan completos en el template (admin, negocio, conexion)
    PASO 4 = configuracion especifica de Control Autolavado -- el IDE lo implementa
    Ver INVESTIGACION_APP.md FASE 5 para definir que campos van en el paso 4
    El paso 4 debe estar completo ANTES de desarrollar modulos de negocio
    -> Implementar en src/setup-wizard/step4/

### DevBadge -- Por Que Es Absolutamente Intocable

  Cada app vendida lleva la barra DevBadge en la parte inferior de toda pantalla.
  Esta es la estrategia de cross-promotion del ecosistema:

    Un cliente compra joshimitzu-autolavado
    -> Ve 'Conoce mas sistemas de gestion' en la barra inferior
    -> Descubre y puede comprar cualquiera de los 44 sistemas
    -> DevBadge es el motor de adquisicion de TODO el ecosistema

  Sin DevBadge cada app es un producto aislado.
  Con DevBadge cada instalacion vende las otras 43 apps.

  REGLA ABSOLUTA:
    - DevBadge NO tiene props de visibilidad
    - Ningun rol, plan, condicion ni URL puede ocultarlo
    - Esta montado en src/app/layout.tsx directamente en el body
    - Cualquier PR que lo modifique sera rechazado por Joshua

### Reglas del Shell Visual

  El codigo del shell YA ESTA en tu repo (clonado desde base-app-template).
  Archivos presentes -- NO modificar su estructura:
    src/components/shell/DashboardShell.tsx    <- wrapper principal
    src/components/shell/DashboardSidebar.tsx  <- sidebar con --brand-color
    src/components/shell/DevBadge.tsx          <- barra inferior INMUTABLE
    src/app/layout.tsx                         <- DevBadge montado aqui
    src/app/globals.css                        <- SOLO cambiar --brand-color

  Unico cambio permitido en globals.css:
    :root { --brand-color: #1d4ed8; }

  Como agregar los modulos de negocio al sidebar (patron obligatorio):

    // En tu layout de dashboard (src/app/(dashboard)/layout.tsx):
    import { DashboardShell, NavItem } from '@/components/shell/DashboardShell'
    import { Users, DollarSign, BarChart2 } from 'lucide-react'

    const NAV_ITEMS: NavItem[] = [
      { href: '/dashboard/clientes', icon: Users,      label: 'Clientes' },
      { href: '/dashboard/pagos',    icon: DollarSign, label: 'Pagos'    },
      { href: '/dashboard/reportes', icon: BarChart2,  label: 'Reportes' },
    ]

    // En el componente del layout:
    <DashboardShell session={session} navItems={NAV_ITEMS}>
      {children}
    </DashboardShell>

  Los modulos exactos los define INVESTIGACION_APP.md FASE 5 (sidebar).
  Siempre usa iconos de lucide-react -- misma libreria en todas las apps.
  NUNCA reimplementar el sidebar desde cero.

### Contexto de Familia

  Miembro de familia Taller/Servicio
  Ecosistema: 44 apps bajo Joshimitzu Software, misma base tecnica, mismo shell

---

## SKILLS DISPONIBLES

  Ubicacion local: E:\Joshimitzu_Projects\02_GlobalUtils\skills\
  Copias en repo : docs/skills/ (SKILL.md por skill)

  Skills asignados a esta app (Taller/Servicio):
    brainstorming, multi-agent-brainstorming, frontend-design, webapp-testing

  CRITICO: Usa el skill 'brainstorming' ANTES de planear cualquier modulo o feature.
  Usa 'multi-agent-brainstorming' para decisiones de arquitectura importantes.

  Como ejecutar un skill en Claude Code:
    /brainstorming           -> lluvia de ideas estructurada
    /multi-agent-brainstorming -> analisis multi-agente
    /frontend-design         -> diseno UI/UX
    /webapp-testing          -> estrategia de pruebas
    /pdf                     -> generacion y exportacion de PDF
    /xlsx                    -> exportacion a Excel

  Ver docs/skills/[nombre]/SKILL.md para el contenido completo de cada skill.

---

## FLUJO DE TRABAJO OBLIGATORIO

  FASE 0 -- Setup (una sola vez):
    1. Leer este archivo INSTRUCCIONES.md
    2. Crear/actualizar tu archivo nativo de instrucciones
    3. Clonar el repo con tu PAT asignado

  FASE 1 -- Investigacion:
    4. Ejecutar /brainstorming para planear la investigacion competitiva
    5. Completar INVESTIGACION_APP.md (5 fases -- ver archivo en el repo)
    6. git checkout -b docs/investigacion-autolavado
    7. git commit + push + PR
    8. Esperar autorizacion: 'si, autorizo' de Joshua

  FASE 2 -- Desarrollo (por cada modulo):
    9. Ejecutar /brainstorming para planear el modulo
   10. Ejecutar /multi-agent-brainstorming para arquitectura si aplica
   11. Escribir tests primero (TDD)
   12. Implementar hasta pasar los tests
   13. PR por cada modulo completado
   14. Esperar aprobacion de Joshua

---

## COMPETIDORES DE REFERENCIA

Investiga los principales sistemas de gestion para: Control Autolavado
Objetivo: identificar 20-30 competidores antes de definir features.

Donde buscar:
  Capterra    : categoria del sector
  G2          : categoria del sector
  MercadoLibre MX: busca 'sistema [sector]'
  Facebook    : grupos del sector en Mexico
  YouTube     : demos de sistemas en espanol

---

## GIT WORKFLOW

  Tipos de commit: feat, fix, docs, refactor, test, chore, perf, ci
  Formato: tipo: descripcion breve en espanol

  Branches:
    docs/investigacion-autolavado    <- investigacion competitiva
    feat/nombre-del-feature     <- nueva funcionalidad
    fix/nombre-del-bug          <- correccion de bug

  Flujo por feature:
    git checkout -b feat/nombre
    git add archivo1 archivo2   (nunca git add . ni git add -A)
    git commit -m 'feat: descripcion del cambio'
    git push origin feat/nombre
    Abrir PR en GitHub
    Esperar aprobacion de Joshua

---

## REFERENCIAS

  Plantilla base : https://github.com/Joshimitzu2000/base-app-template
  Portal         : joshimitzu.com
  API            : api.joshimitzu.com
  Data local     : ~/.joshimitzu/autolavado/

---
*Generado por generar-instrucciones.ps1 -- Joshimitzu Software*