---
slug: es-es/real-world-development/vscode
title: "Visual Studio Code"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

**[GitHub Copilot Chat](https://code.visualstudio.com/docs/copilot/chat/copilot-chat)** en VS Code incorpora GitHub Copilot al editor que ya utilizas. En Visual Studio Code y GitHub Codespaces, dirigirás Copilot Chat en modo agente, conectarás herramientas externas mediante MCP y utilizarás agentes personalizados, todo ello sin salir del IDE, desde el que Copilot puede acceder a tus archivos, al terminal y a los problemas.

Empezarás por añadir instrucciones personalizadas y observar cómo las sigue Copilot. Después, utilizarás el modo agente para desarrollar una funcionalidad de filtrado que incluya la interfaz, la capa de datos y las pruebas. A continuación, conectarás el servidor MCP de Playwright y dejarás que Copilot controle un navegador para probar la funcionalidad antes de abrir una solicitud de incorporación de cambios. Por último, revisarás y utilizarás un agente personalizado para trabajar en la accesibilidad y supervisarás, orientarás e iterarás sobre los cambios de Copilot sin salir del editor.

## Ejercicios

| Ejercicio | Tema | Descripción |
|----------|-------|-------------|
| [0. Requisitos previos][ex0] | Configuración | Crea tu repositorio y codespace |
| [1. Instrucciones personalizadas][ex1] | Contexto | Añade y verifica las instrucciones personalizadas en VS Code |
| [2. Modo agente][ex2] | Generación de código | Desarrolla una funcionalidad de filtrado en modo agente |
| [3. MCP con Playwright][ex3] | Herramientas externas | Prueba la funcionalidad en un navegador con el servidor MCP de Playwright |
| [4. Agentes personalizados][ex4] | Agentes especializados | Revisa y utiliza agentes personalizados |
| [5. Supervisar y gestionar agentes][ex5] | Supervisión | Supervisa y orienta las sesiones de agente |
| [6. Iteración][ex6] | Revisión | Revisa localmente el trabajo de Copilot y elige los siguientes pasos |
| [Opcional: Incorporar Foundry][foundry-toolkit] | Agentes de IA | Prepara un modelo, publica un agente y conéctalo al sitio en tres módulos con VS Code y Foundry Toolkit |

## Requisitos previos

Antes de asistir a este taller, asegúrate de tener:

- [ ] Una cuenta de GitHub con un plan activo **Copilot Student, Pro, Pro+, Business o Enterprise**
- [ ] Acceso a GitHub Codespaces

> [!TIP]
> ¿No tienes un plan de pago? Los estudiantes verificados pueden obtener GitHub Copilot gratis mediante [GitHub Education][callout-student-plan-education]. El plan **Copilot Student** incluye el agente, MCP, la revisión de código y las funciones de Copilot CLI que utiliza este taller; podrás completar todos los itinerarios.

[callout-student-plan-education]: https://github.com/education/students

## Empezar

**[Empieza por el ejercicio 0: Requisitos previos →][ex0]**

[ex0]: 0-prerequisites/
[ex1]: 1-custom-instructions/
[ex2]: 2-agent-mode/
[ex3]: 3-mcp/
[ex4]: 4-custom-agents/
[ex5]: 5-managing-agents/
[ex6]: 6-iterating/
[foundry-toolkit]: 7-foundry-toolkit/
