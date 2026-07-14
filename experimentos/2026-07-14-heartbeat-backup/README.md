# Experimento: Backup integral de un espacio en Heartbeat

- **Fecha:** 2026-07-14
- **Objetivo:** Evaluar la viabilidad de respaldar íntegramente ("todo el espacio") una comunidad
  de Heartbeat (heartbeat.chat) a la que se tiene acceso pagado.
- **Estado:** Investigación inicial (sin construir aún).

## Contexto: qué puede y no puede hacer el agente

- El agente **no** navega ni se autentica como humano con sesión persistente.
- Sí puede **investigar** recursos públicos y **construir herramientas/scripts** que el usuario
  ejecuta con **sus propias credenciales**.
- Comprobado empíricamente: desde el entorno del agente, `api.heartbeat.chat` no responde
  (HTTP 000), mientras que la web pública sí. → El trabajo autenticado debe correr en la máquina
  del usuario.

## Hallazgos de la investigación

### 1. Existe una API oficial (vía legítima)
- Base URL: `https://api.heartbeat.chat/v0`
- Auth: `Authorization: Bearer {api_key}`
- Métodos: GET, POST, PUT, DELETE
- API key: se genera en **Settings > System > API Keys** (típicamente disponible para
  **owners/admins** de la comunidad, no para miembros normales — a confirmar).
- Endpoints conocidos: `GET /users`, `PUT /directMessages`, y endpoints que devuelven posts
  recientes. Falta el catálogo completo (channels, documents, courses, comments).

### 2. Exportación oficial de datos
- Se puede **solicitar al soporte** una exportación → CSV con **Documents, Comments y Posts**.
- No incluye videos. Probablemente disponible solo para el owner de la comunidad.

### 3. Videos nativos = la parte difícil y sensible
- Heartbeat aloja "Native Videos" con **"download prevention"** y **"authentication check on
  video load"** explícitos: están **diseñados para impedir la descarga**.
- Implicación: respaldar videos choca de frente con la protección de la plataforma → terreno de
  ToS y, si hay cifrado/DRM, línea roja legal. **No se construyen mecanismos para romper DRM.**

## La pregunta que lo decide todo: ¿owner o miembro?

- **Si eres owner/admin:** tienes API key + exportación oficial → camino limpio y legítimo para
  texto/posts/documentos. Los videos siguen protegidos, pero son tuyos.
- **Si eres solo miembro que pagó:** no hay API key ni export; solo tienes lo que la UI te muestra.
  Ir más allá pelea contra las protecciones → territorio de ToS.

## Próximos pasos (pendiente de definir con el usuario)

- [ ] Confirmar rol (owner vs miembro).
- [ ] Según rol, decidir alcance: API oficial / export / solo lo accesible por UI.
- [ ] Definir qué se hace (o no) con los videos, respetando ToS y sin romper DRM.
