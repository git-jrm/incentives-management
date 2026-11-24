# Incentives Management

## Contexto
Modernización de un aplicativo *legacy* (incentivos) actualmente en producción para saldar la deuda técnica acumulada y habilitar nuevas funcionalidades solicitadas por el negocio, como mejorar la visibilidad al equipo integrando métricas visuales de cumplimiento en tiempo real mejorando la trazabilidad.

El alcance busca migrar el sistema local hacia una plataforma *cloud* manteniendo la continuidad operativa, mejorando la mantenibilidad e integración del sistema a un proceso eficiente de mejora continua (CI/CD).

## Limitaciones sistema legacy
* **Entorno aislado:** Al funcionar en un entorno local cerrado sin acceso remoto, impide que el administrador supervise el estado y avance de las actividades en tiempo real desde internet.
* **Falta de trazabilidad en omisiones:** El sistema actual solo persiste las actividades ejecutadas, sin dejar registro de las tareas planificadas que no se realizaron.
* **Ausencia de métricas de cumplimiento:** Carece de indicadores visuales rápidos que permitan evaluar el rendimiento general por día y si las tareas se ejecutaron dentro de los bloques horarios esperados.

## Inventario de Funcionalidades (Alcance)

| ID / Funcionalidad | Descripción / Regla de negocio clave | Legacy | Nuevo |
| :--- | :--- | :--- | :--- |
| **F-01** / Planificación semanal | Permite ingresar actividades indicando días de la semana y sus bloques de horario con sus valores (ej. 9=100,10=80). | **Sí** | Sí |
| **F-02** / Dashboard | Muestra tabla semana actual y tabla resumen en la parte superior. | **Sí** | Sí |
| **F-03** / Componente día | Lista actividades registradas (pasado), actividades planificadas y registradas (hoy) ó actividades planificadas (futuro).
| **F-04** / Ejecución de actividad | Las actividades planificadas para el día actual se muestran como un botón que se presiona realizada la actividad. | **Sí** | Sí |
| **F-05** / Tabla resumen | Muestra totales acumulados para mes anterior y semana anterior por cada usuario. | **Sí** | Sí |
| **F-06** / Estado por tarea | Mostrar un emoji junto a cada tarea: en tiempo, fuera de tiempo, o no realizadas (días pasados). | **No** | Sí |
| **F-00** / Resumen diario con nota | Mostrar en la parte superior un emoji por cada día transcurrido a modo de "nota" o calificación general del día. | **No** | Sí |
| **F-07** / Acceso web autenticado | Permitir acceder al sistema de forma autenticada a través de internet. | **No** | Sí |
| **F-01** / Planificación anual | Permite ingresar actividades indicando meses, días del mes y sus bloques de horario con sus valores (ej. 9=100,10=80). | **No** | Sí |
| **F-07** / Pool de actividades | Permitir acceder al sistema de forma autenticada a través de internet. | **No** | Sí |

### Criterio UX y Psicología del Comportamiento (Estados de Actividad)

* **Diseño de estados:** El sistema diferencia el cumplimiento en bloque horario (`☑️`) del cumplimiento fuera de plazo (`✔️`) mediante un indicador neutral, evitando castigar el retraso.
* **Prevención de abandono:** Al ser bloques definidos por el propio usuario, penalizar un retraso con alertas negativas activa la culpa (principal causa de abandono), mientras que premiarlo igual que el cumplimiento puntual diluye la disciplina.
* **Validación sin juicio:** El estado neutral (`✔️` / `🙂`) reconoce el esfuerzo de cumplir el compromiso personal (*progreso sobre perfección*), reservando el máximo refuerzo visual (`☑️` / `😁`) para la puntualidad.
* **Balance del sistema:** Esta escala crea un entorno flexible pero estructurado que fomenta la constancia, educa sin juzgar y maximiza la retención.

**Incentives Management** is an enterprise-grade compensation system that automates performance-based bonus calculations by evaluating daily operational objectives through the OKR (Objectives and Key Results) methodology.

Instead of managing granular tasks, the architecture maps each business day as a high-level **Objective**, where the scheduled daily goals act as quantitative **Key Results**. 

The system features a real-time computation engine that tracks completion rates and time-bound compliance, programmatically triggering financial incentives and bonus eligibility as soon as the daily objective is marked as completed through the fulfillment of its activities (goals).

REQS:
1.- una zona donde hayan actividades ´para elegir´ (que se pueda elegir ´libre´? porqupe?)

This is the MVP wireframe validate with stakeholder:

> * El enfoque usa Late con indicador neutral para los retrasos desde la psicología del comportamiento ya que el usuario define su propio bloque horario, el sistema actúa como un espejo de su compromiso personal, no se debe "castigar" el estado Late con emojis negativos ya que activaría la culpa. Por otro lado, premiar igual que el On Time diluye el valor de la disciplina y fomenta la procrastinación.


#### DESKTOP (spanish)
```text
+--------------------------------------------------------------------------------------------------------------+
| 🔥🔥🔥🔥🔥🔥🔥 | 🔥🔥🔥🙂🔥🔥🔥 | 🔥🙂🔥🔥😐🔥🔥 | 🔥🔥🔥😐🔥🔥🔥 | 🔥🔥🔥         |     <  >     |
+--------------------------------------------------------------------------------------------------------------+
|   sun 1/11  |   mon 2/11  |   tue 3/11  |                wednesday 4/11     | thu 5/11 | fri 6/11 | sat 7/11 |
+-------------+-------------+-------------+-----------------------------------+----------+----------+----------+
| ✅ GOAL (X) | ☑️ GOAL (X) | ☑️ GOAL (X) | [GOAL (X)]  [GOAL (X)]  (FF)  [+] | GOAL (X) | GOAL (X) | GOAL (X) |
| ✅ GOAL (X) | ☑️ GOAL (X) | ☑️ GOAL (X) | [GOAL (X)]  [GOAL (X)]  (MM)  [+] | GOAL (X) | GOAL (X) | GOAL (X) |
| ✅ GOAL (X) | ☑️ GOAL (X) | ☑️ GOAL (X) | [GOAL (X)]  [GOAL (X)]  (JJ)  [+] | GOAL (X) | GOAL (X) | GOAL (X) |
|             | ☑️ GOAL (X) | ☑️ GOAL (X) |                                   | GOAL (X) | GOAL (X) |          |
|             | ☑️ GOAL (X) | ☑️ GOAL (X) | ☑️ GOAL (X)                       | GOAL (X) | GOAL (X) |          |
|             | ☑️ GOAL (X) | ✔️ GOAL (X) | ☑️ GOAL (X)                       |          |          |          |
|             | ✔️ GOAL (X) | ✖️ GOAL (X) | ✔️ GOAL (X)                       |          |          |          |
+-------------+-------------+-------------+-----------------------------------+----------+----------+----------+
| ✅ On-time      ✔️ Late      ✖️ Not done      🔥 All in time      🙂 All done      😐 Something left undone  |
+--------------------------------------------------------------------------------------------------------------+
```

#### MOBILE (spanish)
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
