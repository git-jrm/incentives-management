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
| **FR-01** / Planificación semanal | Permite ingresar actividades recurrentes indicando días de la semana, bloques de horario y valores. | ✅ | ✅ |
| **FR-02** / Planificación adicional | Permite ingresar actividades adicionales y su valor. | ✅ | ✅ |
| **FR-03** / Planificación anual | Permite ingresar actividades recurrentes indicando meses, días del mes y valores. | ❌ | ✅ |
| **FR-04** / Planificación puntual | Permite ingresar actividades puntuales, indicando fecha de inicio, si es persistente y su valor. | ❌ | ✅ |
| **FR-05-old** / Semana actual (legacy) | Tabla en dashboard con actividades de cada `día` de la semana actual, desde el inicio hasta el día actual. | ✅ | ❌ |
| **FR-05** / Semana actual (new) | Tabla en dashboard con actividades de cada `día` de la semana actual completa, de inicio a fin. | ❌ | ✅ |
| **FR-06-old** / Totales (legacy) | Muestra los totales del mes anterior, semana anterior y semana actual. | ✅ | ✅ |
| **FR-06** / Totales (new) | Muestra los totales del mes anterior y mes actual. | ✅ | ✅ |

| **FR-10** /  | Muestra una representación visual por cada día pasado de la semana actual y semanas pasadas, para el estado final del día: . | ❌ | ✅ |


| **FR-06** / Componente `día` | Pasado: actividades `hechas` y `no hechas`; actual: actividades `planificadas` (no hechas), `botón más` y `hechas`; ó futuro: `actividades planificadas`. | ✅ | ✅ |
| **FR-07** / Ejecución de actividad | Las actividades `planificadas` para el día actual se muestran como botones que se presionan al realizar la actividad. | ✅ | ✅ |
| **FR-08** / Tabla resumen | Muestra totales mes anterior y semana anterior por persona. | ✅ | ❌ |
| **FR-09** / Estado actividades registradas | Muestra representación del estado de cada actividad : `hecha a tiempo`, `hecha fuera de tiempo` o `no hecha` (día pasado). | ❌ | ✅ |
| **FR-11** / Acceso web autenticado | Permitir acceder al sistema de forma autenticada a través de internet. | ❌ | ✅ |
| **FR-12** / Botón más | Muestra actividades puntuales y adicionales. | ❌ | ✅ |

### No funcionales

<inserte tabla>

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
| 🔥🔥(🔥)🔥🔥🔥|🔥🔥🔥(🔥)🔥🔥🔥🔥🔥🔥(🔥)🔥🔥🙂🔥🔥🔥(🔥)🙂🔥🔥😐🔥🔥(🔥)🔥🔥😐🔥🔥🔥|(🔥)🔥🔥 |  < 💎 >  |
| MES ACT:                                                                       |         
+--------------------------------------------------------------------------------------------------------------+
|   dom 1/11  |   lun 2/11  |   mar 3/11  |                miércoles 4/11     | jue 5/11 | vie 6/11 | sáb 7/11 |
+-------------+-------------+-------------+-----------------------------------+----------+----------+----------+
| ✅ GOAL (X) | ☑️ GOAL (X) | ☑️ GOAL (X) | [GOAL (X)]  [GOAL (X)]  (FF)  [+] | GOAL (X) | GOAL (X) | GOAL (X) |
| ✅ GOAL (X) | ☑️ GOAL (X) | ☑️ GOAL (X) | [GOAL (X)]  [GOAL (X)]  (MM)  [+] | GOAL (X) | GOAL (X) | GOAL (X) |
| ✅ GOAL (X) | ☑️ GOAL (X) | ☑️ GOAL (X) | [GOAL (X)]  [GOAL (X)]  (JJ)  [+] | GOAL (X) | GOAL (X) | GOAL (X) |
|             | ☑️ GOAL (X) | ☑️ GOAL (X) |                                   | GOAL (X) | GOAL (X) |          |
|             | ☑️ GOAL (X) | ☑️ GOAL (X) | ☑️ GOAL (X)                       | GOAL (X) | GOAL (X) |          |
|             | ☑️ GOAL (X) | ✔️ GOAL (X) | ☑️ GOAL (X)                       |          |          |          |
|             | ✔️ GOAL (X) | ✖️ GOAL (X) | ✔️ GOAL (X)                       |          |          |          |
+-------------+-------------+-------------+-----------------------------------+----------+----------+----------+
| Actividad:  ✅ En tiempo      ✔️ Fuera de tiempo      ✖️ No hecha                                                   |
| Estado día: 🔥 Todo a tiempo      🙂 Todo hecho      😐 Algo no hecho                                        |
+--------------------------------------------------------------------------------------------------------------+
```

#### MOBILE (spanish)
```text
+------------------------------------+
| NOVEMBER 🔥 🙂 😐                  |
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
Indicador meses:
• 👑 Nivel 1 (Impecable): Todo el equipo cumplió el 100% de las tareas y siempre en horario. (Máximo estatus y reconocimiento).
• ⭐ Nivel 2 (Cumplido): Se completó todo el trabajo del mes, aunque algún día hubo entregas fuera de horario. (Buen desempeño, meta lograda sin el estatus perfecto).
• 📝 Nivel 3 (Observaciones): Se avanzó con el plan, quedó algún punto no hecho para ajustar en el próximo ciclo si existe patrón. (Enfoque en mejora continua).


