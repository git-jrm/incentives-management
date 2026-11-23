# Sistema de Gestión y Seguimiento de Actividades

## Contexto
Evolución de un sistema actualmente en producción (hoy funciona de forma aislada/local) hacia una versión web accesible desde internet. El objetivo es mantener intacta la operación diaria actual y sumar visibilidad remota para el administrador mediante indicadores visuales de cumplimiento.

## Inventario de Funcionalidades (Alcance)


| ID / Funcionalidad | Descripción / Regla de negocio clave | Tipo | Estado |
| :--- | :--- | :--- | :--- |
| **F-01** / Planificación recurrente semanal | Ingresar actividad y día/s de la semana a repetir y especificar bloque/s de horario con su valor/es (ej: 8=100,9=80,10=60). | **Actual** | Actual |
| **F-02** / Dashboard semanal | Vista de la semana actual: muestra actividades realizadas en días previos y botones de tareas planificadas para el día de hoy. | **Actual** | Pendiente |
| **F-03** / Ejecución de actividad | El usuario presiona el botón de la actividad al terminarla y esta pasa al listado de realizadas del día actual. | **Actual** | Pendiente |
| **F-04** / Resumen mensual | Mostrar en la parte superior del dashboard los valores acumulados por usuario correspondientes al mes pasado. | **Actual** | Pendiente |
| **F-05** / Acceso web administrador | Permitir al administrador consultar el sistema de forma remota a través de internet (requiere autenticación). | **Nueva** | Pendiente |
| **F-06** / Estado visual por tarea | Mostrar un emoji junto a cada tarea: en tiempo, fuera de tiempo, o "❌" para actividades no realizadas en días pasados. | **Nueva** | Pendiente |
| **F-07** / Resumen diario con nota | Mostrar en la parte superior un emoji por cada día transcurrido a modo de "nota" o calificación general del día. | **Nueva** | Pendiente |

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





