# Hallazgos: respaldo de contenido en Heartbeat

> Fecha de investigación: 2026-07-14. Fuentes: documentación pública de Heartbeat y pruebas de
> conectividad desde el entorno del agente.

## Contexto y rol

- **Plataforma:** heartbeat.chat — plataforma de comunidades, membresías y cursos.
- **Rol del usuario:** **miembro que pagó**, NO owner/admin. Este punto es determinante.

## Capacidades del agente (calibración honesta)

- El agente **no** navega ni se autentica como humano con sesión persistente; no puede iniciar
  sesión con credenciales del usuario ni resolver 2FA.
- Sí puede investigar recursos públicos y **construir herramientas** que el usuario ejecuta con
  **sus propias credenciales** en su máquina.
- **Prueba empírica (2026-07-14):** desde el entorno del agente, `api.heartbeat.chat` no responde
  (HTTP 000); la web pública (`www.heartbeat.chat`) y GitHub sí (200). → El trabajo autenticado
  debe correr en la máquina del usuario.

## Hallazgos técnicos

### 1. API oficial — vía limpia, pero de admin
- Base URL: `https://api.heartbeat.chat/v0` · Auth: `Authorization: Bearer {api_key}`.
- Métodos GET/POST/PUT/DELETE. Endpoints conocidos: `GET /users`, `PUT /directMessages`, posts
  recientes. Catálogo completo no confirmado.
- API key: **Settings > System > API Keys** → panel de administración, típicamente **solo para
  owners/admins**. Un miembro normal **no** tiene acceso a esto.

### 2. Exportación oficial — también de admin
- Se solicita a soporte → CSV con **Documents, Comments y Posts** (sin videos).
- Disponible para el **owner** de la comunidad, no para miembros.

### 3. Videos nativos — protegidos por diseño
- "Native Videos" con **"download prevention"** y **"authentication check on video load"**
  explícitos: pensados para **impedir la descarga**.

## Conclusión para un MIEMBRO

Las dos vías limpias (API y export) son de **administrador**, así que **no están disponibles**
para un miembro. Un miembro solo tiene acceso a lo que la **UI** le muestra.

Implicación: un "respaldo integral del espacio completo" **no es alcanzable por medios limpios**
siendo miembro. Buscarlo por completo implica pelear contra los controles de acceso y los
Términos de Servicio de la plataforma.

## Límites (líneas rojas)

- 🚫 **No romper DRM / cifrado** de videos (ilegal en muchas jurisdicciones).
- ⚠️ **Respetar ToS:** la descarga masiva suele estar prohibida aunque hayas pagado; puede costar
  la cuenta.

## Lo que SÍ es razonable (uso personal)

- Guardar para uso personal **contenido de texto que el usuario puede ver legítimamente** en la UI
  (notas, posts, documentos) — copiar/pegar o exportar lo accesible.
- **No** construir mecanismos que sorteen la "download prevention" de los videos.

## Pendientes / decisiones abiertas

- [ ] Definir con el usuario qué contenido de texto concreto quiere conservar y en qué formato.
- [ ] Decidir explícitamente que los videos protegidos quedan fuera (recomendado).
