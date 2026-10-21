# Completar cursos de certificación con Chrome MCP

Paquete reutilizable para Claude Code, Gemini CLI u otro cliente que pueda controlar Chrome mediante MCP. Su objetivo es descubrir y completar **todo lo que exige el curso**: lecturas, videos, interacciones, laboratorios, proyectos, entregas, quizzes, exámenes y requisitos para emitir el certificado.

Repositorio público: [javier321jg/cursos-certificacion-chrome-mcp](https://github.com/javier321jg/cursos-certificacion-chrome-mcp). Puedes consultar las instrucciones, clonar la skill o descargarla desde **Code → Download ZIP**.

La skill adapta el trabajo a la plataforma y verifica el resultado de cada actividad. No garantiza que todos los cursos puedan completarse íntegramente por un agente: una evaluación supervisada, una validación de identidad o una revisión del instructor puede requerir intervención o espera. El registro conserva esos pendientes sin declararlos completados.

## 1. Preparar la conexión

Necesitas un modelo, un cliente que ejecute herramientas MCP y el [servidor oficial Chrome DevTools MCP](https://github.com/ChromeDevTools/chrome-devtools-mcp). Una conversación web sin herramientas locales no controla automáticamente tu Chrome.

Instala Node.js LTS con npm y Chrome actualizado. Las configuraciones incluidas usan `--autoConnect`, que requiere Chrome 144 o posterior. Abre el perfil de Chrome donde tienes el curso, visita `chrome://inspect/#remote-debugging` y habilita la conexión. Acepta el diálogo de Chrome cuando el MCP solicite conectarse. El servidor accede al perfil conectado; cierra las pestañas privadas ajenas al trabajo.

Consulta el [procedimiento oficial de conexión](https://github.com/ChromeDevTools/chrome-devtools-mcp/blob/main/docs/advanced-usage.md). Para usar un perfil separado, elimina `--autoConnect` de los argumentos: el MCP abrirá su propio Chrome al usar una herramienta y deberás iniciar sesión allí.

## 2. Instalar en tu cliente

Desde la raíz de tu proyecto, elige uno de estos comandos. Requieren Git; si la carpeta de destino ya existe, revisa su contenido antes de instalar.

**Claude Code — PowerShell:**

```powershell
New-Item -ItemType Directory -Path .claude/skills -Force | Out-Null
git clone https://github.com/javier321jg/cursos-certificacion-chrome-mcp.git .claude/skills/cursos-certificacion-chrome-mcp
```

**Gemini CLI — PowerShell:**

```powershell
New-Item -ItemType Directory -Path .gemini/skills -Force | Out-Null
git clone https://github.com/javier321jg/cursos-certificacion-chrome-mcp.git .gemini/skills/cursos-certificacion-chrome-mcp
```

Si prefieres descargar el ZIP, extrae su contenido, renombra la carpeta a `cursos-certificacion-chrome-mcp` y cópiala en la ubicación correspondiente. Conserva `SKILL.md`, las referencias, las configuraciones y la plantilla.

| Cliente | Carpeta de la skill en tu proyecto | Configuración MCP del proyecto |
| --- | --- | --- |
| Claude Code | `.claude/skills/cursos-certificacion-chrome-mcp/` | `.mcp.json` |
| Gemini CLI | `.gemini/skills/cursos-certificacion-chrome-mcp/` | `.gemini/settings.json` |

Para Claude, combina [config/claude-code.windows.json](config/claude-code.windows.json) con tu configuración MCP. Para Gemini, combina [config/gemini.windows.json](config/gemini.windows.json). Conserva los demás ajustes. Reinicia el cliente si es necesario y consulta `/mcp` para comprobar la conexión.

En Claude Code puedes invocar `/cursos-certificacion-chrome-mcp`. En Gemini CLI pide «Usa la skill cursos-certificacion-chrome-mcp» y acepta su activación cuando corresponda. También puedes instalarla en la carpeta personal de skills de cada cliente.

Referencias: [MCP de Claude Code](https://code.claude.com/docs/en/mcp), [skills de Claude Code](https://code.claude.com/docs/en/skills), [MCP de Gemini CLI](https://geminicli.com/docs/tools/mcp-server/) y [skills de Gemini CLI](https://geminicli.com/docs/cli/skills/).

Para otro cliente, importa la configuración según su formato y entrega `SKILL.md` con sus referencias como instrucciones del proyecto. Las capacidades, permisos y reglas dependen del cliente elegido.

## 3. Mensaje para comenzar

Sustituye el enlace y copia este mensaje:

```text
Usa la skill cursos-certificacion-chrome-mcp para completar este curso:
[URL DEL CURSO]. Trabaja en mi Chrome conectado.

Primero descubre todos los requisitos de aprobación y certificación,
y registra su estado. Completa las lecturas, videos, interacciones,
laboratorios, proyectos, entregas, quizzes, exámenes y requisitos
adicionales disponibles dentro de las capacidades y reglas del cliente.
Autorizo los clics, envíos y descargas necesarios dentro del curso.

Continúa por todos los pendientes hasta verificar la emisión del
certificado y descargarlo si la plataforma lo permite. Comprueba cada
resultado guardado y conserva un registro para retomar. Si necesitas
mis datos u opiniones, pídemelos juntos; si un paso exige mi presencia
o una autorización adicional, déjalo identificado y continúa lo demás.
Informa el resultado real y cualquier requisito que siga pendiente.
```

Esta autorización cubre el trabajo indicado dentro del curso. Si quieres publicaciones ante compañeros o solicitudes en otra plataforma de credenciales, indícalo expresamente. Facilita tus respuestas reales a encuestas y cualquier material propio que requieran los proyectos.

## 4. Qué debe comprobar el agente

1. **Inventario:** todos los requisitos, incluidos los ocultos dentro de módulos o desbloqueados después.
2. **Actividades:** progreso guardado de videos, lecturas, ejercicios y laboratorios.
3. **Evaluaciones y entregas:** aprobación confirmada; revisión humana pendiente si corresponde.
4. **Emisión:** certificado emitido y archivo descargado, o motivo concreto por el que todavía no se puede obtener.

El procedimiento detallado está en [references/flujo-completo.md](references/flujo-completo.md). La plantilla [templates/estado.json](templates/estado.json) permite conservar el avance entre sesiones o modelos. El agente debe guardar una copia de trabajo sin sobrescribir la plantilla original.

Para retomar, entrega el registro al nuevo agente y escribe:

```text
Usa la skill cursos-certificacion-chrome-mcp y este registro de avance.
Contrasta el estado con la plataforma y continúa los requisitos pendientes
hasta verificar la credencial. Conserva las actividades ya aprobadas.
```

Guarda tus copias de trabajo, evidencias y certificados fuera del repositorio público. La plantilla incluida está vacía; no publiques registros de tus cursos o documentos personales al contribuir a este proyecto.

## Actualizar la skill

Si la instalaste con Git, ejecuta `git pull --ff-only` dentro de la carpeta de la skill. Conserva tus registros de trabajo fuera de ella. Si modificaste sus instrucciones, revisa esos cambios antes de actualizar. Para proponer una mejora, abre un issue o un pull request en GitHub describiendo el problema y la plataforma afectada, sin adjuntar credenciales, datos personales ni contenido privado del curso.

## Validación y procedencia

El punto de partida fue un curso de NetAcad completado mediante el navegador integrado de Codex. Este paquete generaliza el procedimiento y lo adapta al MCP de Chrome; no se ha ejecutado de principio a fin con Claude o Gemini ni se ha probado en todas las plataformas. Se comprobaron el formato de la skill, los JSON, los enlaces internos y el ZIP. No contiene credenciales ni respuestas prefijadas.

Configuración consultada el 21 de octubre de 2026: [opciones del servidor](https://github.com/ChromeDevTools/chrome-devtools-mcp/blob/main/docs/configuration.md) y [solución de problemas](https://github.com/ChromeDevTools/chrome-devtools-mcp/blob/main/docs/troubleshooting.md). Si no encuentra `npx`, revisa el entorno de Node del cliente; si no encuentra tu sesión, revisa el perfil conectado y la autorización de Chrome. Los ejemplos son para Windows nativo.
