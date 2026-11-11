---
title: "Ejercicio 6 - Iterar sobre el trabajo de GitHub Copilot"
authors:
  - geektrainer
lastUpdated: 2026-06-30
next: false
---

| [← Lección anterior: Supervisar y gestionar agentes][previous-lesson] |
| :-- |

## Revisa el trabajo

Durante este taller has trabajado con GitHub Copilot en varias tareas para mejorar la experiencia de usuario. Has utilizado el modo agente para añadir filtros en el cliente y el servidor, el servidor MCP de Playwright para probar manualmente ese trabajo en un navegador y, después, un agente personalizado para implementar funciones de accesibilidad —modos de alto contraste y claro— y has orientado la sesión mientras seguía activa para ampliar el trabajo. Ahora toca publicar ese trabajo local y revisarlo como lo haría tu equipo.

### Escenario

Los fundamentos del diseño de software y DevOps no cambian con la llegada de la IA generativa. Sigue siendo necesario revisar el trabajo generado por Copilot. Publicaremos los cambios de accesibilidad desde el codespace, abriremos una solicitud de incorporación de cambios y revisaremos las diferencias antes de involucrar al resto del equipo.

## Publica las funciones de accesibilidad

Los modos de alto contraste y claro que implementaste con el agente personalizado de accesibilidad en los [Ejercicios 4][exercise-4] y [5][exercise-5] están en el codespace como cambios confirmados mediante commits. Vamos a publicarlos en una rama y a abrir una solicitud de incorporación de cambios para que el equipo pueda revisarlos.

1. Vuelve al codespace.
2. Abre la vista **Source Control** en VS Code.
3. Confirma que los cambios de accesibilidad están confirmados mediante commits. Si tienes cambios sin confirmar del Ejercicio 5, prepáralos y confírmalos ahora con un mensaje descriptivo, como `Add high-contrast and light-mode toggles`.
4. Publica la rama seleccionando **Publish Branch** (o abre el menú **...** y selecciona **Push**).
5. VS Code ofrecerá abrir la nueva rama en github.com. Acepta la propuesta o ve manualmente al repositorio y selecciona **Compare & pull request** en el aviso de la rama.
6. Escribe un título claro (por ejemplo, `Add high-contrast and light-mode toggles`) y una descripción breve que resuma qué has hecho y por qué.
7. Selecciona **Create pull request**.
8. Cuando se abra la PR, selecciona **Files changed** para revisar todo el trabajo. Presta especial atención a:
   - los componentes de interfaz para alternar entre modos;
   - el uso del almacenamiento local para conservar las preferencias del usuario;
   - los cambios de CSS o de estilo para los modos de alto contraste y claro;
   - los atributos de accesibilidad (etiquetas ARIA, navegación con teclado, etc.);
   - el código JavaScript/TypeScript que gestiona el cambio de modo.

9. Vuelve a la pestaña **Conversation**.
10. Si hay flujos de trabajo pendientes de aprobación, selecciona **Approve and run workflows**.

    ![Aprobar y ejecutar flujos de trabajo](../../../_images/shared-approve-workflows.png)

11. Espera a que terminen los flujos. Si todo va bien, deberían superarse.

> [!TIP]
> ¿Quieres una segunda opinión sobre el trabajo de accesibilidad? Menciona a `@copilot` en un comentario de la PR con una petición como «revisa esta PR para detectar otros problemas de WCAG» o «sugiere mejoras en el orden de navegación con teclado». Copilot iniciará una nueva sesión para atender el comentario.

## Ejercicio opcional: sigue explorando en local

Trabajar de forma iterativa con un agente en el IDE es una habilidad que solo se desarrolla con la práctica. Puedes probar estas ideas en futuras sesiones de VS Code:

- añadir un formulario de interés para patrocinadores en la página de detalles del juego;
- implementar la paginación en la página de la lista de juegos;
- añadir validación de entradas y gestión de errores a los asistentes de acceso a datos de `src/lib/`;
- ampliar el alcance del agente de accesibilidad; por ejemplo, revisar el orden del foco del teclado en todo el sitio.

## Resumen

Enhorabuena. Has completado el itinerario de VS Code. En este taller:

- **Has utilizado MCP de Playwright para probar manualmente la funcionalidad.** Has añadido el servidor MCP de Playwright y dejado que Copilot manejara un navegador para comprobar el filtrado antes de abrir una solicitud de incorporación de cambios.
- **Has dirigido el modo agente en cambios coordinados en todas las capas.** Has añadido una funcionalidad de filtrado que afecta al cliente, al servidor y a las pruebas en una sola sesión.
- **Has utilizado un agente personalizado.** Has seleccionado el agente personalizado de accesibilidad en el selector de agentes y observado cómo implementaba el modo de alto contraste en el repositorio.
- **Has gestionado y orientado una sesión de agente.** Has revisado los cambios propuestos en el propio editor, aceptado los que querías y ampliado la sesión con una indicación de seguimiento para añadir el modo claro.
- **Has cerrado el ciclo con una solicitud de incorporación de cambios.** Has publicado el trabajo local y lo has revisado de principio a fin como lo haría tu equipo.

## Revisión y siguientes pasos

Aquí termina el itinerario obligatorio de VS Code. El taller ya está completo y puedes parar.

Si quieres ampliar tu perspectiva sobre las capacidades de los agentes de Copilot, los demás itinerarios presentan escenarios relacionados en otros entornos:

- 💻 **[Itinerario de CLI](../../cli/)**: entrega dos cambios revisados desde el terminal con los modos Plan y Autopilot, habilidades, un agente QA personalizado, MCP de Playwright, Agent Merge y traspasos basados en el contexto.
- ☁️ **[Itinerario del agente en la nube](../../cloud/)**: asigna incidencias al agente en la nube, supervisa las sesiones desde la página de agentes e itera de forma asíncrona sobre las solicitudes de incorporación de cambios.

También puedes seguir ampliando lo que has empezado aquí. [awesome-copilot][awesome-copilot] es una buena fuente de archivos de instrucciones, agentes personalizados y habilidades que puedes adaptar a tus proyectos.

Como ampliación opcional, [Opcional: Incorporar Foundry][exercise-7] utiliza VS Code y Microsoft Foundry Toolkit para preparar un modelo, implementar un Backer Concierge y conectarlo al sitio.

## Recursos

- [GitHub Copilot][github-copilot]
- [Copilot Chat en VS Code][copilot-chat-vscode]
- [Uso del modo agente][agent-mode]

---

| [← Lección anterior: Supervisar y gestionar agentes][previous-lesson] |
|:--|

[previous-lesson]: ../5-managing-agents/
[exercise-4]: ../4-custom-agents/
[exercise-5]: ../5-managing-agents/
[exercise-7]: ../7-foundry-toolkit/
[github-copilot]: https://github.com/features/copilot
[copilot-chat-vscode]: https://code.visualstudio.com/docs/copilot/chat/copilot-chat
[agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
[awesome-copilot]: https://github.com/github/awesome-copilot
