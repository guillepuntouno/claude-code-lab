# Bitácora del Agente

> Documento vivo. Al abrirlo debes entender **qué** hacemos, **cómo** lo hacemos y **por qué**.
> Se actualiza cada vez que exploramos una capacidad nueva o tomamos una decisión relevante.

---

## Contexto general

- **Propósito:** Explorar y documentar las capacidades de Claude Code como agente de código en distintos frentes de trabajo.
- **Repositorio:** https://github.com/guillepuntouno/claude-code-lab (público).
- **Estado inicial:** Directorio vacío. No era repositorio git.
- **Idioma de trabajo:** Español.
- **Inicio:** 2026-07-14

### ¿Por qué existe este documento?
Para que cualquier sesión futura (o cualquier persona) pueda abrir este archivo y entender el
contexto de lo que se ha hecho, las decisiones tomadas y el razonamiento detrás de ellas, sin
tener que reconstruirlo desde cero.

---

## Cómo trabajamos (convenciones)

- **Qué / Cómo / Por qué:** cada entrada del registro documenta esas tres dimensiones.
- **Fechas absolutas:** siempre en formato `AAAA-MM-DD`.
- **Formato:** Markdown tradicional, legible tanto en crudo como renderizado.
- **Sin datos sensibles:** este repo es **público**. No se commitean correos, tokens, rutas
  internas/corporativas, nombres de servidores ni credenciales. Los secretos van en archivos
  ignorados por git (ver `.gitignore`).

---

## Registro de actividades

### 2026-07-14 — Creación de la bitácora

- **Qué:** Se crea `BITACORA.md` como documento base de contexto.
- **Cómo:** Tras inspeccionar el directorio (vacío, sin git), se genera este archivo con
  secciones de contexto, convenciones y registro cronológico.
- **Por qué:** Establecer desde el arranque un lugar único donde quede el conocimiento de la
  herramienta y de las pruebas que vayamos haciendo.

### 2026-07-14 — Repositorio git + GitHub

- **Qué:** Se convierte el directorio en repositorio git y se publica en GitHub (repo público).
- **Cómo:** `git init` en rama `main`, `.gitignore` que excluye configuración local y secretos.
  El repo remoto se creó en github.com y se conectó con `git remote add` + `push`.
  Autenticación vía Personal Access Token pasado de forma efímera (sin persistirlo en `origin`);
  el token se guarda localmente en un archivo ignorado por git.
- **Por qué:** Tener historial de versiones de todo lo que experimentemos y un lugar público donde
  quede el conocimiento. Se eligió nombre tipo "lab" para comunicar que es un espacio de
  experimentación, no de producción.

### 2026-07-14 — Saneamiento de datos sensibles

- **Qué:** Se retiran de la documentación el correo, la ruta interna y otras referencias sensibles.
- **Cómo:** Reescritura de `BITACORA.md` en términos genéricos y nueva convención "sin datos
  sensibles".
- **Por qué:** El repositorio es público; los secretos y datos internos no deben quedar en el
  historial de git.

### 2026-07-14 — Reescritura de historial y estructura del repo

- **Qué:** Se elimina todo dato sensible del historial de git y se crea la estructura de carpetas
  del laboratorio.
- **Cómo:** `git filter-branch` reescribió el correo del autor (→ `noreply` de GitHub) y saneó el
  contenido de los `.md` en todos los commits; se limpiaron backups (`refs/original`), reflog y
  `gc`, seguido de `push --force`. Se añadieron `README.md` de portada, carpetas `docs/`
  (con `frentes/`, `capacidades/`, `guias/`), `scripts/`, `experimentos/` y `plantillas/` con
  plantillas base.
- **Por qué:** Sanear el archivo actual no basta: los datos seguían en commits antiguos de un repo
  público. La estructura separa lo cronológico (bitácora) de lo temático (`docs/`) y da un lugar
  claro para scripts, experimentos y plantillas.

---

## Capacidades exploradas

<!-- Se irá llenando conforme probemos cada frente. Ejemplo de plantilla:

### <Nombre de la capacidad>
- **Qué es:**
- **Cómo se usa:**
- **Cuándo conviene:**
- **Notas / hallazgos:**
-->

### Web / investigación autónoma (2026-07-14)
- **Qué es:** Con `WebSearch` y `WebFetch` puedo investigar recursos públicos y con `curl`
  comprobar conectividad, pero **no** navego con sesión autenticada ni inicio sesión como humano.
- **Cómo se usa:** Para investigar plataformas y **construir herramientas** que el usuario ejecuta
  con sus propias credenciales.
- **Limitaciones:** Centros de ayuda con anti-bot devuelven 403 a `WebFetch`; hosts de API pueden
  no responder al agente. El trabajo autenticado corre en la máquina del usuario, no en la mía.
- **Notas:** Primer uso real en el frente Heartbeat (ver `docs/frentes/heartbeat/`).

---

## Registro de actividades (cont.)

### 2026-07-14 — Primer experimento: investigación de Heartbeat

- **Qué:** Investigar la viabilidad de respaldar íntegramente una comunidad de Heartbeat.
- **Cómo:** Búsquedas web + comprobación de conectividad. Hallazgos documentados en
  `docs/frentes/heartbeat/` y `experimentos/2026-07-14-heartbeat-backup/`.
- **Por qué / conclusión:** El usuario es **miembro** (no owner), así que las vías limpias (API y
  export) —que son de administrador— no aplican. Un respaldo integral no es alcanzable por medios
  limpios; los videos están protegidos contra descarga por diseño. Se fijan límites: no romper DRM
  ni sortear protecciones; sí es razonable conservar para uso personal el texto accesible en la UI.

---

## Pendientes / Ideas a explorar

- [ ] Heartbeat: definir qué contenido de texto conservar y en qué formato.
