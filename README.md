# Gestión de Incentivos y Actividades

## Contexto
Modernización de un aplicativo *legacy* (gestión de incentivos) actualmente en producción para saldar la deuda técnica acumulada y habilitar nuevas funcionalidades solicitadas por el negocio, como mejorar la visibilidad al equipo integrando métricas visuales de cumplimiento en tiempo real para la trazabilidad.

El alcance busca migrar el sistema local hacia una plataforma *cloud* manteniendo la continuidad operativa, mejorando la mantenibilidad e integración del sistema a un proceso eficiente de mejora continua (CI/CD).

## Limitaciones sistema legacy
* **Falta de trazabilidad en omisiones:** El sistema actual solo persiste las actividades ejecutadas, sin dejar registro de las tareas planificadas que no se realizaron.
* **Operación aislada (sin acceso remoto):** Al funcionar en un entorno local cerrado, impide que el administrador supervise el estado y avance de las actividades en tiempo real desde internet.
* **Ausencia de métricas de cumplimiento:** Carece de indicadores visuales rápidos que permitan evaluar si las tareas se ejecutaron dentro de los bloques horarios esperados o el rendimiento general por día.

## Limitaciones sistema legacy
* **Entorno aislado:** Funciona de forma local sin conexión; el nuevo sistema requiere acceso remoto por internet con autenticación para el administrador.
* **Sin registro de omisiones:** Solo guarda las actividades ejecutadas al presionar el botón, pero **no registra las actividades no realizadas**. El nuevo sistema debe contrastar lo planificado vs. lo ejecutado para mostrar las "❌" en días pasados y calcular la nota diaria.

## Inventario de Funcionalidades (Alcance)

| ID / Funcionalidad | Descripción / Regla de negocio clave | Legacy | Nuevo |
| :--- | :--- | :--- | :--- |
| **F-01** / Planificación semanal | Permite ingresar actividades, indicando los días de la semana y bloques de horario con sus valores (ej. 8=100,9=80,10=60). | **Sí** | Sí |
| **F-02** / Dashboard semanal | Muestra el total del mes anterior por colaborador y una tabla con la semana actual. | **Sí** | Sí |
| **F-03** / Componente día | Fecha pasada actividades planificadas registradas, fecha actual actividades planificadas no registradas y registradas, fecha futura actividades planificadas

Tabla con los días de la semana actual: muestra actividades para cada día realizadas en días previos y botones de tareas planificadas para el día de hoy. | **Sí** | Sí |

| **F-03** / Ejecución de actividad | El usuario presiona el botón de la actividad al terminarla y esta pasa al listado de realizadas del día actual. | **Sí** | Sí |
| **F-04** / Resumen mensual | Mostrar en la parte superior del dashboard los valores acumulados por usuario correspondientes al mes pasado. | **Sí** | Sí |
| **F-05** / Acceso web administrador | Permitir al administrador consultar el sistema de forma remota a través de internet (requiere autenticación). | **No** | Sí |
| **F-06** / Estado visual por tarea | Mostrar un emoji junto a cada tarea: en tiempo, fuera de tiempo, o "❌" para actividades no realizadas en días pasados. | **No** | Sí |
| **F-07** / Resumen diario con nota | Mostrar en la parte superior un emoji por cada día transcurrido a modo de "nota" o calificación general del día. | **No** | Sí |

## Diseño Técnico (Borrador)
* **Frontend:** [Por definir]
* **Backend:** [Por definir]
* **Base de Datos:** [Por definir]
* **Seguridad:** [Ej. Login simple con usuario/contraseña para el administrador]

## Cómo levantar el proyecto
*(Completar cuando inicie el desarrollo)*
---

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





