# Bitácora del Agente

> Documento vivo. Al abrirlo debes entender **qué** hacemos, **cómo** lo hacemos y **por qué**.
> Se actualiza cada vez que exploramos una capacidad nueva o tomamos una decisión relevante.

---

## Contexto general

- **Propósito:** Explorar y documentar las capacidades de Claude Code como agente de código en los distintos frentes de trabajo de Guillermo.
- **Directorio de trabajo:** `<directorio-local>`
- **Estado inicial:** Directorio vacío (solo `.claude/settings.local.json`). No es repositorio git.
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

---

## Registro de actividades

### 2026-07-14 — Creación de la bitácora

- **Qué:** Se crea `BITACORA.md` como documento base de contexto.
- **Cómo:** Tras inspeccionar el directorio (vacío, sin git), se genera este archivo con
  secciones de contexto, convenciones y registro cronológico.
- **Por qué:** Establecer desde el arranque un lugar único donde quede el conocimiento de la
  herramienta y de las pruebas que vayamos haciendo.

### 2026-07-14 — Repositorio git + GitHub

- **Qué:** Se convierte el directorio en repositorio git y se prepara para publicarse en GitHub
  (repo público en la cuenta personal `<correo-omitido>`).
- **Cómo:** `git init` en rama `main`, identidad local configurada, `.gitignore` que excluye
  `settings.local.json` (config personal) y ruido de SO/editores. Primer commit con la bitácora.
  El repo remoto lo crea Guillermo en github.com y luego se conecta con `git remote add` + `push`.
  Publicado en **https://github.com/guillepuntouno/claude-code-lab**.
  Autenticación: el entorno no tiene `gh` ni credenciales cacheadas; el push se hizo con un
  Personal Access Token (fine-grained, scope *Contents: Read and write*) pasado de forma efímera
  sin persistirlo en `origin` ni en disco.
- **Por qué:** Tener historial de versiones de todo lo que experimentemos y un lugar público donde
  quede el conocimiento. Se eligió nombre tipo "lab" para comunicar que es un espacio de
  experimentación, no de producción.

---

## Capacidades exploradas

<!-- Se irá llenando conforme probemos cada frente. Ejemplo de plantilla:

### <Nombre de la capacidad>
- **Qué es:**
- **Cómo se usa:**
- **Cuándo conviene:**
- **Notas / hallazgos:**
-->

_Aún sin entradas._

---

## Pendientes / Ideas a explorar

- [ ] Definir los "diferentes frentes" de trabajo a probar.
