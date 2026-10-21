# Adaptador para Chrome DevTools MCP

Lee los esquemas expuestos por el servidor conectado antes de llamar herramientas. Los nombres siguientes se verificaron en la [referencia oficial](https://github.com/ChromeDevTools/chrome-devtools-mcp/blob/main/docs/tool-reference.md); los prefijos del cliente y los parámetros pueden variar por versión.

| Necesidad | Herramienta habitual | Uso en el curso |
| --- | --- | --- |
| Localizar pestaña | `list_pages` | Reconocer dominio y título |
| Seleccionar pestaña | `select_page` | Usar el `pageId` observado |
| Leer controles | `take_snapshot` | Obtener texto y UID actuales |
| Abrir curso | `navigate_page` | Navegar al enlace aportado |
| Elegir opción | `click` | Usar UID de la última instantánea |
| Rellenar un control | `fill` | Aplicar el valor admitido por su esquema |
| Esperar texto visible | `wait_for` | Confirmar avance sin esperas arbitrarias |
| Conservar evidencia | `take_screenshot` | Capturar el resultado final necesario |

Ejemplo de secuencia, con variables obtenidas de las respuestas del servidor:

```text
list_pages()
P := pageId de la pestaña cuyo dominio y título corresponden al curso
select_page({pageId: P, bringToFront: true})
take_snapshot({pageId: P})
U := uid del control correcto en esa instantánea
click({pageId: P, uid: U, includeSnapshot: true})
```

Esto es pseudocódigo, no un script ejecutable: el cliente hace las llamadas MCP. `P` y `U` no son identificadores literales. No reutilices UID después de una navegación o cambio de vista.

En páginas con contenido incrustado, comprueba el árbol de accesibilidad de la actividad. Si una instantánea no muestra sus controles, usa una captura y la herramienta de inspección que admita el servidor; no deduzcas respuestas de contenido oculto. Si el cliente no puede interactuar con ese marco, informa la limitación concreta. No cambies a llamadas internas de progreso.

Las configuraciones incluidas son para Windows nativo. En macOS/Linux, el comando suele ser `npx` y se eliminan los dos primeros argumentos, `/c` y `npx`, del arreglo de Windows; se conserva `-y` y lo que sigue. Usa la instalación de Chrome y Node del mismo entorno. No presupongas que WSL puede adjuntarse al Chrome de Windows con la misma configuración.
