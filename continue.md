# Continue · Banco Galicia + Salesforce — Deck para la DEMO

> **Última actualización:** 2026-08-11
> **Estado:** Estable / listo para revisar. Deck funcional de 11 slides, servido local.
> **Ubicación:** `~/claude-projects/GALICIA - Presesntacion para la DEMO/`

---

## 1. Resumen ejecutivo

Presentación HTML interactiva (deck de slides estilo keynote) **Banco Galicia × Salesforce**,
sobre la estrategia de transformación del modelo de atención comercial (PyME + Renta Alta) con
foco en **estrategia agéntica** (Agentforce, FSC, Data Cloud, Tableau Next, Slack).

- **Origen:** clonado del asset original en Heroku
  (`https://bago-life-sciences-0344e7c91182.herokuapp.com/`, basic auth `galicia:galicia-7856`).
  Ese deck tenía 31 slides (storytelling largo por actos con Martín/Valentina). **Se recortó a
  6 slides** y luego **se expandió a 11** sumando bloque de estrategia agéntica + impacto + cierre.
- **Estado actual:** 11 slides, self-contained (sin CDN, sin scripts remotos), corre 100% offline.
- **Decisión clave:** **se mantiene LOCAL, no se publica** (contenido de cliente real; el usuario
  descartó GitHub Pages / repo público para evitar indexación en buscadores).
- **NO es un repo git** todavía (decisión deliberada — sin versionado por ahora).

---

## 2. Tech stack

- **HTML + CSS + JS vanilla** en un solo archivo (`index.html`, ~1695 líneas).
- Sin frameworks, sin build, sin dependencias externas.
- **Fuentes reales de Salesforce** embebidas localmente (`assets/fonts/*.woff`: AvantGarde for
  Salesforce + Salesforce Sans).
- Fondos animados: dos `<canvas>` (`#fieldBg` light-field, `#veilBg` LineWaves WebGL) — vienen
  del asset original, no se tocaron.
- Navegación por JS: `document.querySelectorAll(".slide")` → flechas ← →, barra espaciadora,
  `F` fullscreen. **Al agregar/borrar slides la navegación se auto-ajusta** (no hay lista
  hardcodeada de slides en el JS).

---

## 3. Estructura del repo

```
GALICIA - Presesntacion para la DEMO/
├── index.html                  # el deck completo (11 slides)
├── continue.md                 # este archivo
├── Contexto de Galicia.pdf     # brief del cliente (fuente de slides 4 y 6)
├── .DS_Store                   # (ruido macOS, ignorable)
└── assets/
    ├── fonts/       (5)  AvantGarde + Salesforce Sans (.woff)
    ├── logos/       (2)  banco-galicia.svg + galicia-wordmark.svg
    ├── personas/    (4)  martin, tomas, valentina, cafe-del-plata (.jpg)
    ├── video/       (2)  galicia-reunion-cafe.mp4, galicia-taxi-dictado.mp4  ← HUÉRFANOS (ver §7)
    ├── crm/         (1)  valentina-360.jpg  ← HUÉRFANO
    ├── mobile/      (1)  rm-home-cuentas.png ← HUÉRFANO
    ├── img/         (2)  agentic-systems.png, ask-agentforce.png ← portados de Consorcio
    └── salesforce-logo.svg
```

---

## 4. Los 11 slides (orden actual)

| # | data-slide | Título / esencia | Origen |
|---|-----------|------------------|--------|
| 01 | `cover` | Portada "Banco Galicia + Salesforce" + firma | Galicia orig (editado) |
| 02 | `gracias` | Keynote "Gracias" | Galicia orig |
| 03 | `fls` | Forward-Looking Statements | Galicia orig (editado) |
| 04 | `punto-partida` | "Dónde estamos hoy" — 6 dolores en tarjetas **naranjas** | PDF Contexto |
| 05 | `raquel` | Demo — **Raquel, Cliente Eminent de Alto Valor** | nuevo (persona) |
| 06 | `solucion` | "La solución propuesta" — 6 pilares en tarjetas **celestes** | PDF Contexto |
| 07 | `sf-agentic-proof` | "Salesforce ya es una Empresa Agéntica" (4M+, $130M, 203K, 300+) | Consorcio adaptado |
| 08 | `cinco-sistemas` | "Necesita cinco sistemas" (Engagement/Agency/Work/Insight/Context) | Consorcio adaptado |
| 09 | `arquitectura-agentica` | "Arquitectura de empresa agéntica para el banco" (imagen) | Consorcio adaptado |
| 10 | `proof` | "El impacto, probado" — casos First Horizon / RBC | Galicia orig |
| 11 | `thanks` | Cierre "Ejecutivo potenciado, cliente contento" | Galicia orig (editado) |

**Numeración:** cada slide tiene `<div class="slide-number">NN / 11</div>` **hardcodeado**.
Si agregás/quitás un slide, hay que renumerar TODOS a mano (o con el snippet de §10).

---

## 5. Fuentes de contenido

- **Slides 4 y 6** (Punto de Partida + Solución): salen de `Contexto de Galicia.pdf` (era un
  Google Doc privado `1tzevMR0WINtGhX0nd_sdHwJfjvVvBsNs03mR6SvW8aQ`, se compartió como PDF en
  la carpeta). Contenido literal: 7 dolores → se dejaron 6 (se quitó "Planificación manual");
  5 pilares de solución → se agregó un 6º ("Gestión comercial proactiva").
- **Slides 7, 8, 9** (estrategia agéntica): portados del deck
  `~/claude-projects/CONSORCIO - PoV Corredora de Seguros/consorcio-corredora-premium.html`
  (slides 5, 8 y 14 de ese deck), adaptados de Seguros → Banca/Galicia.
- **Slides 10 y 11**: recuperados del asset original de Galicia (`/tmp/bago_asset.html`, ya no
  disponible tras reinicio — el original vive en Heroku).

---

## 6. CSS / clases clave (para editar sin romper)

Todo el CSS vive en el `<head>` (`<style>` grande antes de línea ~715). Clases reutilizables:

- **Tarjetas dolor/solución:** `.grid-3` + `.info-card`. Variante `.pain` = naranja/coral
  (dolores, slide 4); variante `.sol` = celeste con glow (solución, slide 6). La clase `.pain`
  se agregó a mano (usa `--leg-4: #E0714C`, la paleta que el deck reservaba para "pains").
- **Persona (slide 5):** `.persona`, `.p-photo`, `.p-badge`, `.p-quote`, `.p-wounds`/`.p-wound`.
- **Estrategia agéntica (portado):** `.five` + `.sys-card` (cinco sistemas), `.cy-grad`
  (gradiente cyan animado con `@keyframes hue` que ya existía), `.arch-img` (imagen arquitectura),
  `.split` + `.stat-2x2` + `.img-wrap` (slide SF agéntica).
- **Proof (slide 10):** `.proof`, `.pf-grid`, `.pf-stat`, `.pf-bench`. Los números usan
  `<span class="count" data-target="N" data-suffix="..." data-prefix="...">` — un JS los anima
  con count-up al entrar al slide.
- **Cierre (slide 11):** `.thanks`, `.thanks-lockup`, `.accent` (dorado), `.byline`.
- **Portada (slide 1):** `.cover-wrap` (centrado vertical), `.cover-sign` (firma anclada abajo,
  `position:absolute; left:84px; bottom:64px`).

Paleta (CSS vars en `:root`): `--gold`/`--gold-lt` (highlights), `--cy`/`--cy-lt` (accent
estructural cyan), `--leg-4` #E0714C (coral, dolores). Dark premium: `--bg` #080B16, `--ink` #F4F1E9.

---

## 7. Gotchas / deuda técnica conocida

1. **Código muerto (~500 líneas).** Al recortar de 31→6 slides se borraron secciones pero
   quedó su CSS y JS huérfano en el `<head>` y al final del `<body>`: reglas de `.reunion-video`,
   `.ph-stage` (overlay del celular), `.br-container` (briefing), handlers de video, etc. **Son
   inofensivos** (los handlers JS tienen guardas `if (!el) return`), pero ensucian el archivo.
   PENDIENTE opcional: limpiar con `/simplify` o a mano.
2. **Assets huérfanos.** `video/*.mp4` (~5MB), `crm/valentina-360.jpg`, `mobile/rm-home-cuentas.png`
   ya no se referencian en el HTML (eran de las slides borradas). Se pueden eliminar para
   aligerar la carpeta. **CSS aún referencia `mobile/rm-home-cuentas.png`** en reglas `.ph-screen`
   / `.pho-screen` (muertas) — si borrás el archivo no rompe nada visible.
3. **Imágenes portadas de Consorcio (Seguros).** `assets/img/agentic-systems.png` (slide 9) y
   `assets/img/ask-agentforce.png` (slide 7) vienen del deck de seguros. **Revisar que no tengan
   branding/texto de seguros** que desentone en contexto Galicia/Banca. El de arquitectura
   (`agentic-systems.png`) muestra la pila Agentforce/Slack/Tableau sobre Customer 360 —
   conceptualmente sirve, pero verificar el texto embebido en la imagen.
4. **Numeración manual.** Los `slide-number` son hardcodeados `NN / 11`. Agregar/quitar slides
   requiere renumerar todo (ver snippet §10).
5. **Casos de proof (slide 10).** Números de First Horizon / RBC Wealth Management son casos
   FINS reales de salesforce.com/customers, NO de Galicia. Confirmar que sirven para el pitch.
6. **Persona Raquel — foto.** Usa `assets/personas/valentina.jpg`. El foco se reorientó: es
   **Cliente Eminent de Alto Valor** (no PyME); el dato de ser CEO de Café del Plata (cuenta PyME)
   es secundario y funciona como "gancho de riesgo de doble impacto".
7. **`.DS_Store`** en root y en `assets/` — ruido macOS, borrable.

---

## 8. Historial de cambios aplicados (esta sesión)

1. Clonado completo del asset Heroku → local (HTML + 16 assets con basic auth).
2. Recorte de 31 → 6 slides (Apertura, Gracias, FLS, Punto de Partida, Demo·Raquel, Solución).
3. FLS: nombres ilustrativos → "Tienda de Café S.R.L. / Raquel".
4. Slide 4 (dolores): 7 → 6 tarjetas (quitada "Planificación manual"); recoloreadas a naranja.
5. Slide 6 (solución): 5 → 6 pilares (agregado "Gestión comercial proactiva").
6. Slide 5 (Raquel): reenfocada a Cliente Eminent de Alto Valor + atención en el momento justo;
   dato secundario CEO Café del Plata (doble impacto).
7. Sumado bloque agéntico: SF Empresa Agéntica (7), Cinco Sistemas (8), Arquitectura (9) —
   portados de Consorcio.
8. Sumado Impacto en bancos (10) y Cierre (11) del Galicia original.
9. Portada: quitado kicker "Modelos de Atención..." y las 5 fichas de producto; agregada firma
   "Buenos Aires, Agosto 2026 / Equipo de Ingeniería de Soluciones · Salesforce LATAM" anclada
   al bottom.
10. Cierre (11): título en 2 líneas, "Agentforce actúa" en línea propia, quitado botón "Hablemos
    próximos pasos", reordenado el subtítulo.
11. Subtítulo portada: "Del operar y reaccionar al asesorar y anticipar: una estrategia para
    liberar al ejecutivo y potenciar el crecimiento de cada relación."

---

## 9. Pendientes (en orden sugerido)

1. **Revisar visualmente slides 7 y 9** — confirmar que las imágenes portadas de Consorcio no
   tengan branding de seguros que desentone.
2. **Confirmar números del slide 10** (First Horizon / RBC) — ¿sirven para el pitch a Galicia
   o se reemplazan por benchmarks más cercanos?
3. **(Opcional) Limpiar código muerto** — CSS/JS huérfano de las slides borradas (~500 líneas)
   y assets sin usar (video/, crm/, mobile/).
4. **(Opcional) Decidir deploy final** — hoy es local. Si se necesita URL para la demo:
   Heroku con basic auth (como el original) es lo más seguro para contenido de cliente.
   GitHub Pages quedó descartado (indexable/público).

---

## 10. Cómo arrancar una sesión nueva

```bash
cd "~/claude-projects/GALICIA - Presesntacion para la DEMO"

# Servir local para previsualizar
python3 -m http.server 8799
# → abrir http://localhost:8799  (flechas ← → para navegar, F fullscreen)
```

**Renumerar slides** tras agregar/quitar (ejemplo, si el total pasa a 12):
```bash
python3 - <<'PY'
import re
t = open('index.html').read()
# ajustá el nuevo total y renumerá manualmente los slide-number en orden
# (no hay auto-numeración; cada <div class="slide-number">NN / TOT</div> es literal)
PY
```

**Re-descargar un asset del original** (si hiciera falta algo borrado):
```bash
curl -u "galicia:galicia-7856" \
  "https://bago-life-sciences-0344e7c91182.herokuapp.com/assets/RUTA" -o assets/RUTA
```

---

## 11. Persona / tono

- **Idioma:** español (LATAM), registro **ejecutivo pero concreto** — nada informal.
- **Storytelling:** Desafío (Punto de Partida) → Solución → Estrategia agéntica → Impacto → Cierre.
- **Cliente:** Banco Galicia (Argentina), banca PyME + Renta Alta. Contenido de discovery real
  → tratar como confidencial (por eso NO se publica).
- **Persona demo:** Raquel — Cliente Eminent de Alto Valor, CEO de Tienda/Café del Plata S.R.L.

---

## 12. Referencias externas

| Recurso | Ubicación |
|---|---|
| Asset original (Heroku) | `https://bago-life-sciences-0344e7c91182.herokuapp.com/` (auth `galicia:galicia-7856`) |
| Brief de cliente | `./Contexto de Galicia.pdf` (ex Google Doc `1tzevMR0WINtGhX0nd_sdHwJfjvVvBsNs03mR6SvW8aQ`) |
| Deck fuente estrategia agéntica | `~/claude-projects/CONSORCIO - PoV Corredora de Seguros/consorcio-corredora-premium.html` |

---

## 13. Frase de arranque para la próxima sesión

> "Retomo el deck de Banco Galicia (`~/claude-projects/GALICIA - Presesntacion para la DEMO/`).
> Leé `continue.md` primero. Es un deck HTML de 11 slides, local, sin git. Quiero seguir
> ajustando [contenido / limpiar código muerto / revisar imágenes portadas]. Serví local con
> `python3 -m http.server 8799` para previsualizar."
