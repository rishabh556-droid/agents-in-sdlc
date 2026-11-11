---
title: "Lección 1 - Instalar la aplicación GitHub Copilot"
description: "Instala la aplicación GitHub Copilot, conecta el repositorio que has creado a partir de la plantilla, familiarízate con el espacio de trabajo y prueba un chat rápido."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

La **[aplicación GitHub Copilot][about-copilot-app]** es una aplicación de escritorio para desarrollar con agentes. Está basada en GitHub Copilot CLI y se integra de forma nativa con GitHub, por lo que los repositorios, las ramas y las canalizaciones de CI funcionan directamente. Está diseñada para flujos de trabajo en los que diriges varios agentes en paralelo, cada uno en su propio espacio de trabajo aislado, en lugar de hacer todo el trabajo tú mismo, y automatizas tareas repetitivas. Ya tienes Node.js instalado y una copia del proyecto preparada; ahora instalarás la aplicación y conectarás el repositorio.

En esta lección:

- instalarás la aplicación GitHub Copilot e iniciarás sesión;
- añadirás el proyecto a la aplicación desde su repositorio de GitHub;
- te familiarizarás con el espacio de trabajo y con el backlog incluido en la plantilla;
- probarás un chat rápido para conocer mejor la aplicación.

## Escenario

Tu equipo está adoptando agentes de IA para gestionar un backlog cada vez mayor. La aplicación Copilot permite dirigir ese trabajo desde un mismo lugar: elegir incidencias, ejecutar agentes, revisar cambios y combinar solicitudes de incorporación de cambios. En esta lección instalarás y conectarás la aplicación y aprenderás a iniciar una conversación sobre el proyecto.

> [!NOTE]
> Necesitas un plan de Copilot apto: Copilot Free, Copilot Student o cualquier plan de pago (Pro, Pro+, Business o Enterprise). Si utilizas Copilot Business o Copilot Enterprise, el administrador debe mantener habilitada la directiva **GitHub Copilot app**.

## Instala y configura la aplicación GitHub Copilot

Para utilizar la aplicación GitHub Copilot, primero debes instalarla. Hay versiones para Windows, macOS y Linux. Vamos a instalar la aplicación, autenticarla y añadir el repositorio Tailspin Toys.

1. En un navegador, abre la [página de la aplicación GitHub Copilot][download-app].
2. Descarga la aplicación para tu plataforma e instálala siguiendo las instrucciones de la página.
3. Abre la aplicación una vez instalada.
4. Selecciona **Sign in to GitHub** y sigue las instrucciones para autenticarte. Si utilizas GitHub Enterprise Cloud con residencia de datos, selecciona **Use GitHub Enterprise** y, cuando se te solicite, introduce el nombre de host `*.ghe.com`. GitHub Enterprise Server no es compatible.
5. Si durante la configuración se te pide que selecciones un repositorio, selecciona el repositorio Tailspin Toys que has creado a partir de la plantilla. También puedes omitir la selección y añadir el proyecto después.
6. Cuando se te solicite, elige un tema y termina la configuración.
7. Busca el repositorio en **Sessions**, en la barra lateral. Si ya aparece, no hace falta volver a añadirlo.
8. Si el repositorio todavía no está conectado, selecciona **+** junto a **Sessions** para crear una sesión y, después, selecciona **Add GitHub repository**. Introduce el propietario y el nombre del repositorio que anotaste en la lección de requisitos previos.
9. Comprueba que el repositorio aparece en la barra lateral. En la disposición que se muestra aquí, las carpetas de repositorio, como `tailspin-toys`, están agrupadas en **Sessions** y las sesiones individuales aparecen debajo de cada repositorio.

## Familiarízate con el espacio de trabajo

Cuando el proyecto esté conectado, dedica unos minutos a conocer la aplicación. La barra lateral organiza sus funciones en varias áreas:

- **New**: como cabe esperar, permite iniciar una sesión de chat con Copilot.
- **Pull requests**: muestra las solicitudes de incorporación de cambios mediante la integración nativa con GitHub. Desde aquí puedes explorarlas y filtrarlas, consultar el estado de CI y revisarlas sin salir de la aplicación.
- **Issues**: muestra las incidencias. Puedes explorarlas y filtrarlas e iniciar una sesión a partir de una incidencia.
- **Automations**: tareas guardadas de agentes que se ejecutan según un horario o a petición. Son útiles para gestionar listas de tareas, realizar mantenimiento periódico u otras tareas rutinarias. El repaso las presenta como siguiente paso, no como otro ejercicio del taller.
- **Customize**: permite añadir funciones a la aplicación Copilot, como servidores MCP, complementos, habilidades y otros componentes. La utilizarás para configurar MCP de Playwright.
- **Chats**: conversaciones sencillas para preguntas y sesiones de ideas que no necesitan una rama ni un espacio de trabajo propios. Esta sección aparece después de iniciar el primer chat. Si no está visible, selecciona **+** junto a **Sessions** para iniciar un chat.
- **Sessions**: agrupa las carpetas de los repositorios y las sesiones de agente. Selecciona el nombre de un repositorio, como `tailspin-toys`, para abrir su vista, o selecciona una sesión debajo para volver a esa conversación. Cada sesión se ejecuta en su propio espacio de trabajo aislado; así puedes tener varias sesiones activas sin que sus cambios se mezclen. Iniciarás la primera sesión al añadir valoraciones por estrellas.

Explorarás el espacio de trabajo a medida que avances en el taller.

> [!TIP]
> Si tienes dudas, pregunta a Copilot. Si no sabes cómo hacer algo o si es posible, puede ayudarte.

### Encuentra el backlog precargado

Es probable que todos los proyectos tengan un backlog; Tailspin Toys no es una excepción. Vamos a explorar el backlog creado al generar el proyecto a partir de la plantilla.

1. En **Sessions**, en la barra lateral, selecciona la carpeta del repositorio Tailspin Toys, no una sesión individual. Después, selecciona **Issues** en la navegación superior del repositorio.
2. Busca estas incidencias por su título, no des por hecho que tienen un número concreto:

   - Allow users to filter games by category and publisher
   - Update our repository coding standards

3. Selecciona una incidencia y lee los detalles. Cada incidencia también permite iniciar una sesión de agente. Después de hacer un primer cambio rápido, empezarás por la incidencia de filtrado.

> [!NOTE]
> Las listas de **Issues** y **Pull requests** se filtran automáticamente para mostrar solo los elementos de los repositorios que has añadido a la aplicación Copilot. Para ver elementos de otros repositorios, añádelos a la aplicación.

## Prueba un chat rápido

Una buena forma de familiarizarte con la aplicación es utilizarla para conocer la propia aplicación. Un **chat rápido** es ideal: permite hacer una pregunta o proponer ideas sin crear una rama ni un árbol de trabajo, por lo que puedes hacer una pregunta rápida sin iniciar una sesión.

1. En la barra lateral, selecciona **+** junto a **Chats** para abrir un chat. Si **Chats** aún no está visible, selecciona **+** junto a **Sessions** para iniciar el primer chat; después aparecerá **Chats**.
2. Pregunta cómo funcionan las sesiones de la aplicación:

   ```plaintext
   How does the GitHub Copilot app use worktrees?
   ```

3. Lee la respuesta en la vista de conversación. Cada sesión se ejecuta en su propio árbol de trabajo aislado de Git; esto permite tener varios agentes en paralelo sin que sus cambios se mezclen. Puedes continuar la conversación o iniciar otra cuando quieras.

## Resumen y siguientes pasos

Enhorabuena. Has instalado la aplicación GitHub Copilot, conectado el proyecto y explorado el espacio de trabajo. Has aprendido a:

- instalar la aplicación e iniciar sesión en GitHub;
- añadir un proyecto desde su repositorio de GitHub;
- familiarizarte con el espacio de trabajo y encontrar el backlog en **Issues**;
- utilizar un chat rápido para hacer una pregunta puntual.

A continuación, [iniciarás tu primera sesión de agente][next-lesson] y la utilizarás para mostrar valoraciones por estrellas en las tarjetas de juegos.

## Recursos

- [Acerca de la aplicación GitHub Copilot][about-copilot-app]
- [Introducción a la aplicación GitHub Copilot][getting-started]
- [Trabajar con sesiones de agente en la aplicación GitHub Copilot][agent-sessions]

[next-lesson]: ../2-add-star-rating/
[about-copilot-app]: https://docs.github.com/copilot/concepts/agents/github-copilot-app
[getting-started]: https://docs.github.com/copilot/how-tos/github-copilot-app/getting-started
[agent-sessions]: https://docs.github.com/copilot/how-tos/github-copilot-app/agent-sessions
[download-app]: https://gh.io/app
