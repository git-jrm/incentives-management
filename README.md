# Incentives Management

## Contexto
Modernización del aplicativo *legacy* `incentivos` actualmente en producción, para saldar la deuda técnica acumulada y habilitar nuevas funcionalidades solicitadas por el negocio, como mejorar la visibilidad al equipo integrando métricas visuales de cumplimiento en tiempo real mejorando la trazabilidad.

El alcance busca migrar el sistema local hacia una plataforma *cloud* manteniendo la continuidad operativa, mejorando la mantenibilidad e integración del sistema a un proceso eficiente de mejora continua (CI/CD).

## Limitaciones sistema legacy
* **Entorno aislado:** Al funcionar en un entorno local cerrado sin acceso remoto, impide que el administrador supervise el estado y avance de las actividades en tiempo real desde internet.
* **Planificación semanal:** El sistema actual permite la planificación de actividades recurrentes con frecuencia semanal, se requiere agregar capacidad mensual y anual.
* **Ausencia de métricas de cumplimiento:** Carece de indicadores visuales rápidos que permitan evaluar el rendimiento general por día y si las tareas se ejecutaron dentro de los bloques horarios esperados.
* **Falta de trazabilidad en omisiones:** El sistema actual solo persiste las actividades ejecutadas, sin dejar registro de las tareas planificadas que no se realizaron.

## Requerimientos (Alcance)

### Funcionales

| ID / Funcionalidad | Descripción / Regla de negocio clave | Actual (Legacy) | Nuevo |
| :--- | :--- | :--- | :--- |
| **FR-01** / Planificación semanal | Permite ingresar actividades recurrentes indicando días de la semana, bloques de horario y valores. | Sí | Sí |
| **FR-02** / Planificación adicional | Permite ingresar actividades adicionales y su valor. | Sí | Sí |
| **FR-03** / Planificación anual | Permite ingresar actividades recurrentes indicando meses, días del mes y valores. | **No** | Sí |
| **FR-04** / Planificación puntual | Permite ingresar actividades puntuales, indicando fecha de inicio, si es persistente y su valor. | **No** | Sí |
| **FR-05** / Dashboard | Muestra actividades por cada `día` de la semana actual y un resumen de los totales por persona. | Sí | Sí |
| **FR-06** / Componente `día` | Pasado: actividades `hechas` y `no hechas`; actual: actividades `planificadas` (no hechas), `botón más` y `hechas`; ó futuro: `actividades planificadas`. | Sí | Sí |
| **FR-07** / Ejecución de actividad | Las actividades `planificadas` para el día actual se muestran como botones que se presionan al realizar la actividad. | Sí | Sí |
| **FR-08** / Tabla resumen | Muestra totales mes anterior y semana anterior por persona. | Sí | Sí |
| **FR-09** / Estado actividades registradas | Muestra representación del estado de cada actividad : `hecha a tiempo`, `hecha fuera de tiempo` o `no hecha` (día pasado). | **No** | Sí |
| **FR-10** / Estado semanal | Muestra representación por cada día de la semana (actual y pasadas) para el estado final del día: . | **No** | Sí |
| **FR-11** / Acceso web autenticado | Permitir acceder al sistema de forma autenticada a través de internet. | **No** | Sí |
| **FR-12** / Botón más | Muestra actividades puntuales y adicionales. | **No** | Sí |

### No funcionales

<inserte tabla aquí>

## Criterio UX y Psicología del Comportamiento (Estados de Actividad)

* **Diseño de estados:** El sistema diferencia el cumplimiento en bloque horario (`☑️`) del cumplimiento fuera de plazo (`✔️`) mediante un indicador neutral, evitando castigar el retraso.
* **Prevención de abandono:** Al ser bloques definidos por el propio usuario, penalizar un retraso con alertas negativas activa la culpa (principal causa de abandono), mientras que premiarlo igual que el cumplimiento puntual diluye la disciplina.
* **Validación sin juicio:** El estado neutral (`✔️` / `🙂`) reconoce el esfuerzo de cumplir el compromiso personal (*progreso sobre perfección*), reservando el máximo refuerzo visual (`☑️` / `😁`) para la puntualidad.
* **Balance del sistema:** Esta escala crea un entorno flexible pero estructurado que fomenta la constancia, educa sin juzgar y maximiza la retención.
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
| 🔥 All in time    🙂 All done      |
| 😐 Something left undone           |
+------------------------------------+
```
