# Gestión de Incentivos y Actividades

## Contexto
Modernización de un aplicativo *legacy* (gestión de incentivos) actualmente en producción para saldar la deuda técnica acumulada y habilitar nuevas funcionalidades solicitadas por el negocio, como mejorar la visibilidad al equipo integrando métricas visuales de cumplimiento en tiempo real mejorando la trazabilidad.

El alcance busca migrar el sistema local hacia una plataforma *cloud* manteniendo la continuidad operativa, mejorando la mantenibilidad e integración del sistema a un proceso eficiente de mejora continua (CI/CD).

## Limitaciones sistema legacy
* **Entorno aislado:** Al funcionar en un entorno local cerrado sin acceso remoto, impide que el administrador supervise el estado y avance de las actividades en tiempo real desde internet.
* **Falta de trazabilidad en omisiones:** El sistema actual solo persiste las actividades ejecutadas, sin dejar registro de las tareas planificadas que no se realizaron.
* **Ausencia de métricas de cumplimiento:** Carece de indicadores visuales rápidos que permitan evaluar el rendimiento general por día y si las tareas se ejecutaron dentro de los bloques horarios esperados.

## Inventario de Funcionalidades (Alcance)

| ID / Funcionalidad | Descripción / Regla de negocio clave | Legacy | Nuevo |
| :--- | :--- | :--- | :--- |
| **F-01** / Planificación semanal | Permite ingresar actividades, indicando los días de la semana y bloques de horario con sus valores (ej. 8=100,9=80,10=60). | **Sí** | Sí |
| **F-02** / Dashboard semanal | Tabla semana actual y tabla resumen mes anterior por colaborador. | **Sí** | Sí |
| **F-03** / Componente día | Actividades registradas (fecha pasada), actividades pendientes (botones) y registradas (fecha actual) ó actividades planificadas (fecha futura).
| **F-04** / Ejecución de actividad | El usuario presiona el botón de la actividad al terminarla y esta pasa al listado de registradas del día actual. | **Sí** | Sí |
| **F-00** / Resumen mensual | Mostrar en la parte superior del dashboard los valores acumulados por usuario correspondientes al mes pasado. | **Sí** | Sí |
| **F-00** / Acceso web administrador | Permitir al administrador consultar el sistema de forma remota a través de internet (requiere autenticación). | **No** | Sí |
| **F-00** / Estado visual por tarea | Mostrar un emoji junto a cada tarea: en tiempo, fuera de tiempo, o "❌" para actividades no realizadas en días pasados. | **No** | Sí |
| **F-00** / Resumen diario con nota | Mostrar en la parte superior un emoji por cada día transcurrido a modo de "nota" o calificación general del día. | **No** | Sí |


# Incentives Management

## Overview

**Incentives Management** is an enterprise-grade compensation system that automates performance-based bonus calculations by evaluating daily operational objectives through the OKR (Objectives and Key Results) methodology.

Instead of managing granular tasks, the architecture maps each business day as a high-level **Objective**, where the scheduled daily goals act as quantitative **Key Results**. 

The system features a real-time computation engine that tracks completion rates and time-bound compliance, programmatically triggering financial incentives and bonus eligibility as soon as the daily objective is marked as completed through the fulfillment of its activities (goals).

REQS:
1.-
2.-
3.- una zona donde hayan actividades ´para elegir´ (que se pueda elegir ´libre´? porqupe?)

This is the MVP wireframe validate with stakeholder:

#### DESKTOP
```text
+--------------------------------------------------------------------------------------------------------------+
| OCTOBER 😁 🙂 😁 🙂 😁 🙂 😁 🙂 😁 🙂 😁 🙂 😁 🙂 😁 🙂 😁 🙂 😁 🙂 😁 🙂 😁 🙂 😁 🙂 😁 🙂 😁             |
| NOVEMBER 😁 🙂 😐                                                                                            |
+--------------------------------------------------------------------------------------------------------------+
|   sun 1/11  |   mon 2/11  |   tue 3/11  |                wednesday 4/11     | thu 5/11 | fri 6/11 | sat 7/11 |
+-------------+-------------+-------------+-----------------------------------+----------+----------+----------+
| ☑️ GOAL (X) | ☑️ GOAL (X) | ☑️ GOAL (X) | [GOAL (X)]  [GOAL (X)]  (FF)  [+] | GOAL (X) | GOAL (X) | GOAL (X) |
| ☑️ GOAL (X) | ☑️ GOAL (X) | ☑️ GOAL (X) | [GOAL (X)]  [GOAL (X)]  (MM)  [+] | GOAL (X) | GOAL (X) | GOAL (X) |
| ☑️ GOAL (X) | ☑️ GOAL (X) | ☑️ GOAL (X) | [GOAL (X)]  [GOAL (X)]  (JJ)  [+] | GOAL (X) | GOAL (X) | GOAL (X) |
|             | ☑️ GOAL (X) | ☑️ GOAL (X) |                                   | GOAL (X) | GOAL (X) |          |
|             | ☑️ GOAL (X) | ☑️ GOAL (X) | ☑️ GOAL (X)                       | GOAL (X) | GOAL (X) |          |
|             | ☑️ GOAL (X) | ✔️ GOAL (X) | ☑️ GOAL (X)                       |          |          |          |
|             | ✔️ GOAL (X) | ✖️ GOAL (X) | ✔️ GOAL (X)                       |          |          |          |
+-------------+-------------+-------------+-----------------------------------+----------+----------+----------+
| ☑️ In-time      ✔️ Done      ✖️ Not done      😁 All in time      🙂 All done      😐 Something left undone  |
+--------------------------------------------------------------------------------------------------------------+
```

#### MOBILE
```text
+------------------------------------+
| NOVEMBER 😁 🙂 😐                  |
+------------------------------------+
|           wednesday 4/11           |
+------------------------------------+
| [GOAL (X)]  [GOAL (X)]  (FF)  [+]  |
| [GOAL (X)]  [GOAL (X)]  (MM)  [ ]  |
| [GOAL (X)]  [GOAL (X)]  (JJ)  [ ]  |
|                                    |
| ☑️ GOAL (X)                        |
| ☑️ GOAL (X)                        |
| ✔️ GOAL (X)                        |
+------------------------------------+
| ☑️ In-time   ✔️ Done   ✖️ Not done |
| 😁 All in time    🙂 All done      |
| 😐 Something left undone           |
+------------------------------------+
```

Each GOAL have own and range of values for example:
- 9:00 - 10:00 hrs : 20000
- 10:00 - 11:00 hrs : 16000
- 11:00 - 12:00 hrs : 15000
- 12:00 - 13:00 hrs : 14000





