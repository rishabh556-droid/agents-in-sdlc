---
title: "Lección 3 - Modos de agente: Plan y Autopilot"
description: "Explora los modos de agente: utiliza Plan para acordar un enfoque, Autopilot para desarrollar el filtrado a partir de una incidencia e Interactive para revisar y verificar el resultado."
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

Hemos empezado por añadir una pequeña funcionalidad al proyecto, pero los cambios más amplios necesitan un proceso más robusto. La aplicación GitHub Copilot está diseñada para adaptarse al flujo de trabajo de una organización y ayudarnos a desarrollar lo correcto y de la manera adecuada. Esta es la primera de varias lecciones en las que seguirás un proceso de desarrollo habitual con agentes: partirás de una incidencia para desarrollar una nueva funcionalidad, comprobarás que el código es válido y que se comporta como esperas y, por último, la combinarás correctamente en el proyecto.

> [!NOTE]
> Utilizarás la misma sesión durante todo el flujo de trabajo de la funcionalidad. Lo habitual sería utilizar sesiones o PR diferentes para cada tipo de archivo, pero haremos una excepción para centrarnos en los conceptos principales.

En esta lección:

- iniciarás una sesión de agente a partir de una incidencia de GitHub;
- definirás los requisitos en modo **Plan**;
- implementarás la funcionalidad en modo **Autopilot**;
- revisarás el código;
- validarás manualmente la funcionalidad en un lienzo del navegador.

Mientras desarrollas esta funcionalidad, actualizarás las instrucciones del repositorio, personalizarás la habilidad `quality-checks` existente, añadirás validación MCP, crearás un agente QA y abrirás la PR de la funcionalidad.

## Escenario

El catálogo de Tailspin Toys está creciendo y los visitantes necesitan filtrar los juegos por categoría y editor. La incidencia del backlog describe la funcionalidad, pero es necesario acordar algunos detalles antes de programar, como la posibilidad de combinar categorías. Utilizarás el modo Plan para resolver estas decisiones y, después, autorizarás una implementación acotada con Autopilot.

## Contexto

La incorporación de agentes de programación con IA no cambia los fundamentos del desarrollo. De hecho, los hace aún más importantes. La mayoría de los desarrolladores siguen un flujo parecido a este:

1. Abrir una incidencia registrada con los detalles del trabajo.
2. Planificar lo que se debe desarrollar.
3. Escribir y revisar el código.
4. Ejecutar las pruebas para validar el código.
5. Validar manualmente la nueva funcionalidad.
6. Crear una solicitud de incorporación de cambios (PR).
7. Combinar el código cuando se haya revisado y se hayan superado las comprobaciones de integración continua.

> [!NOTE]
> Los detalles concretos dependen del equipo y de la organización, pero la mayoría de los procesos siguen un patrón parecido al anterior.

Si sigues este enfoque estándar, te asegurarás de que el código generado por IA cumpla los requisitos y pase por el mismo proceso de revisión que el código escrito manualmente.

## Modos de sesión

El **modo de sesión** determina el nivel de autonomía del agente. Puedes seleccionarlo en el menú desplegable debajo del campo de indicación y cambiarlo en cualquier momento:

- **Interactive**: trabajas con el agente. Propone cambios y espera tus indicaciones antes de continuar.
- **Plan**: el agente crea primero un plan. Revisas y apruebas el plan antes de que lo ejecute.
- **Autopilot**: el agente trabaja de forma totalmente autónoma: escribe código, ejecuta pruebas e itera sin esperar indicaciones.

Empieza en el modo Plan, revisa el plan y, después, utiliza Autopilot para implementarlo.

## Inicia una sesión a partir de la incidencia

Antes de empezar, confirma que la PR de valoraciones por estrellas se ha combinado y que la rama local `main` está actualizada.

1. En **Sessions**, en la barra lateral, selecciona la carpeta del repositorio Tailspin Toys y, después, **Issues** en la navegación superior del repositorio. Abre **Allow users to filter games by category and publisher**. Es una incidencia precargada; no tienes que crear otra.
2. Selecciona **New session** y elige un **new working tree** basado en `main`, ya actualizado.

    ![Vista de la incidencia en la aplicación GitHub Copilot, con una flecha que señala el botón New session](../../../_images/app-new-session-from-issue.png)

3. Confirma que la incidencia está adjunta a la sesión y selecciona **Plan** en el selector de modos.

> [!NOTE]
> Si no se encuentra Node.js o npm, pide al agente que ejecute `node --version` y `npm --version`. Si funcionan en tu terminal, pero no en la sesión, comprueba la configuración de `PATH` o del gestor de versiones de la aplicación y ciérrala por completo antes de volver a abrirla. Reintenta la operación y las comprobaciones que hayan fallado. No reinstales npm solo porque el agente no lo encuentre.

## Planifica la funcionalidad de filtrado

La planificación te permite revisar el enfoque antes de que Copilot escriba código. Como has iniciado la sesión desde la incidencia, Copilot ya tiene el contexto de la solicitud. Envía:

```plaintext
Build this feature.
```

Responde a las preguntas de Copilot y compara el plan con los criterios de aceptación de la incidencia. Comprueba que incluye el filtrado por categoría y editor, controles accesibles, cambios en el acceso a datos y pruebas. Habla con Copilot sobre cualquier comportamiento que no esté claro, como la combinación de varias categorías o qué ocurre cuando no hay juegos que coincidan.

El plan debe incluir lint, pruebas unitarias, pruebas E2E y comprobación de tipos con las herramientas existentes del proyecto. Limítalo a implementar y probar el filtrado; crearás la PR después de completar el flujo de calidad. Pide cambios en el plan antes de aprobarlo y guarda la URL de la incidencia y las aclaraciones acordadas para utilizarlas en la validación posterior.

## Aprueba explícitamente Autopilot

Cuando estés conforme con el plan, selecciona **Approve and implement this plan** o la opción equivalente en la versión instalada. Comprueba qué modo está activo; no des por hecho que la aprobación cambia de modo. Confirma que el indicador muestra **Autopilot**.

Copilot empezará a trabajar en la implementación. Seguirá el plan establecido, generará código y ejecutará pruebas.

> [!NOTE]
> Al aprobar el plan, la implementación puede empezar inmediatamente; revísalo antes. Si Copilot informa de dependencias ausentes o de un conflicto de puertos, resuelve el problema de configuración antes de dar por terminadas las comprobaciones. Detén solo los servidores que hayas iniciado tú.

## Revisa y verifica la implementación

Como cualquier otro código, el resultado generado debe revisarse antes de combinarlo. Revisaremos el código y ejecutaremos el sitio para comprobar que funciona.

1. Abre **Changes** e inspecciona la implementación del filtrado y las pruebas.
2. Compara el resultado con la incidencia y las aclaraciones aprobadas, incluida la combinación de categorías y editores. Comprueba que los cambios siguen las instrucciones del repositorio.
3. Inspecciona los resultados de lint, las pruebas unitarias, las pruebas E2E y la comprobación de tipos. Una comprobación omitida no cuenta como superada.
4. Resuelve los errores y vuelve a ejecutar las comprobaciones afectadas antes de aceptar la implementación. La configuración E2E de Playwright compila y sirve una vista previa, y puede reutilizar un servidor local. Asegúrate de que el servidor probado pertenece a este árbol de trabajo y no a una lección anterior.

## Prueba la nueva funcionalidad

El código parece correcto, pero ¿se ejecuta? Inicia la aplicación como antes y abre el sitio en un lienzo del navegador.

1. Utiliza esta indicación para pedir a Copilot que inicie la aplicación y abra la página en el lienzo:

    ```plaintext
    Start the app and open it in the browser canvas.
    ```

2. Al cabo de unos instantes, se iniciará la aplicación y aparecerá un navegador dentro de la aplicación Copilot.
3. Selecciona una categoría y confirma que los resultados coinciden. Borra el filtro, selecciona un editor y comprueba que los resultados coinciden con él.
4. Combina los filtros de categoría y editor y compara los resultados con la incidencia y el plan aprobado. Si se admiten varias categorías, comprueba el comportamiento acordado.
5. Prueba una combinación sin juegos coincidentes y revisa el estado vacío. Borra o restablece los filtros y confirma que vuelve a aparecer la lista completa.
6. Cuando termines, pide a Copilot que detenga el servidor de desarrollo que ha iniciado para esta sesión:

    ```plaintext
    Stop the dev server and close the browser canvas.
    ```

## Conserva esta sesión para las siguientes lecciones

Todavía no crees ni combines la PR de filtrado. Conserva esta sesión, este árbol de trabajo y esta rama para las lecciones 4 a 8. En la lección siguiente aplicarás instrucciones personalizadas al código de filtrado y, después, añadirás mejoras de la habilidad y de QA antes de crear y combinar la PR conjunta en la lección 8. Puedes dejar la sesión inactiva después de detener el servidor de desarrollo y retomarla en la siguiente lección.

## Resumen y siguientes pasos

Has utilizado distintos modos de agente para desarrollar y revisar una funcionalidad. En esta lección:

- has iniciado una sesión de agente a partir de una incidencia de GitHub;
- has definido los requisitos en modo **Plan**;
- has implementado la funcionalidad en modo **Autopilot**;
- has revisado el código;
- has validado manualmente la funcionalidad en un lienzo del navegador.

A continuación, profundizarás en cómo generar código de acuerdo con las prácticas documentadas [mediante instrucciones personalizadas][next-lesson].

## Recursos

- [Trabajar con sesiones de agente en la aplicación GitHub Copilot][agent-sessions]

[next-lesson]: ../4-custom-instructions/
[agent-sessions]: https://docs.github.com/copilot/how-tos/github-copilot-app/agent-sessions
