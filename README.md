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

| ID / Código / Nombre | Descripción / Regla de negocio | Actual (Legacy) | Nuevo |
| :--- | :--- | :--- | :--- |
| **FR-01** / Planificación semanal | Permite ingresar actividades recurrentes indicando días de la semana, bloques de horario y valores. | ✅ | ✅ |
| **FR-02** / Planificación adicional | Permite ingresar actividades adicionales y su valor. | ✅ | ✅ |
| **FR-03** / Planificación anual | Permite ingresar actividades recurrentes indicando meses, días del mes y valores. | ❌ | ✅ |
| **FR-04** / Planificación puntual | Permite ingresar actividades puntuales (kanban), indicando fecha de inicio, si es persistente y su valor. | ❌ | ✅ |
| **FR-05-old** / Semana actual (legacy) | Tabla en dashboard con actividades de cada `día` de la semana actual, desde el inicio hasta el día actual. | ✅ | ❌ |
| **FR-05** / Semana actual (new) | Muestra en dashboard con actividades de cada `día` de la semana actual completa, de inicio a fin. | ❌ | ✅ |
| **FR-06-old** / Componente `día` (old) | Pasado: actividades `hechas`; actual: actividades `planificadas` (no hechas), `botón más` y `hechas`; ó futuro: nada. | ✅ | ❌ |
| **FR-06** / Componente `día` (new) | Pasado: actividades `hechas` y `no hechas`; actual: actividades `planificadas` (no hechas), `botón más` y `hechas`; ó futuro: `actividades planificadas`. | ❌ | ✅ |
| **FR-07** / Ejecución de actividad | Las actividades `planificadas` para el día actual se muestran como botones que se presionan y pasan al listado de actividades `hechas`. | ✅ | ✅ |
| **FR-08** / Representación actividad registrada | Muestra representación visual del estado de cada actividad : `hecha a tiempo`, `hecha fuera de tiempo` o `no hecha` (día pasado). | ❌ | ✅ |
| **FR-09** / Representación día | Muestra una representación visual de cada estado de los últimos días pasados. | ❌ | ✅ |
| **FR-10** / Representación mes | Muestra una representación visual de cada estado de los últimos meses pasados. | ❌ | ✅ |
| **FR-11-old** / Totales (legacy) | Muestra en dashboard los montos totales y directos; del mes anterior, semana anterior y semana actual. | ✅ | ❌ |
| **FR-11** / Totales (new) | Muestra en dashboard los montos totales del mes anterior y mes actual. | ❌ | ✅ |
| **FR-12** / Acceso web autenticado | Permitir acceder al sistema de forma autenticada a través de internet. | ❌ | ✅ |
| **FR-13** / Botón día libre | Marcar día libre evita actividades no hechas. | ❌ | ✅ |
| **FR-14** / Botón más | Muestra botón día libres, actividades puntuales y adicionales. | ❌ | ✅ |

## Indicadores

### Indicador mes
• 👑 Nivel 1 (Impecable): Todo el equipo cumplió el 100% de las tareas en horario. (Máximo estatus y reconocimiento).
• 🪙 Nivel 2 (Cumplido): Se completó todo el trabajo del mes, aunque algún día hubo entregas fuera de horario. (Buen desempeño, meta lograda sin el estatus perfecto).
• 📝 Nivel 3 (Observaciones): Se avanzó con el plan, quedó algún punto no hecho para ajustar en el próximo ciclo si existe patrón. (Enfoque en mejora continua).

### Indicador día
• En horario: Floreció 🌻: Se completaron todas las actividades dentro de su bloque horario establecido. (disciplina y excelencia).
• Fuera de horario: 🌱 Germinó: Compromiso cumplido, completadas todas las actividades, con alguna fuera de bloque. (Cumplimiento sobre perfección).
• Con margen: 🥀 Marchitó: Se avanzó con la jornada, quedando alguna actividad pendiente para calibrar en la planificación. (Concientización y progreso).

### Indicador actividad
• ✅ Hecha a tiempo: Ejecutada dentro de su bloque horario.
• ☑️ Hecha fuera de tiempo: Ejecutada durante el día, pero fuera de su bloque horario.
• ✖️ No hecha: Actividad planificada que no se ejecutó al cierre del día.

#### Desktop view
```text
+--------------------------------------------------------------------------------------------------------------+
|  <                                últimos 40 días                                  >   |  <ultimos 3 meses>  |
|  🌻🌻🌻🌻🌻(🌻🌻🌻🌻🌻🌻🌻🌻🌻🌱🌻🌻🌻🌻🌱🌻🌻🌻🥀🌻🌻🌻🌻🌻🌻🌻🌱🌻🌻🌻🌻)🌻🌱🥀   |      👑  💎  🪙     |
+--------------------------------------------------------------------------------------------------------------+
|   dom 1/11  |   lun 2/11  |   mar 3/11  |            miércoles 4/11         | jue 5/11 | vie 6/11 | sáb 7/11 |
+-------------+-------------+-------------+-----------------------------------+----------+----------+----------+
| ✅ GOAL (X) | ✅ GOAL (X) | ✅ GOAL (X) | [GOAL (X)]  [GOAL (X)]  (FF)  [+] | GOAL (X) | GOAL (X) | GOAL (X) |
| ✅ GOAL (X) | ✅ GOAL (X) | ✅ GOAL (X) | [GOAL (X)]  [GOAL (X)]  (MM)  [+] | GOAL (X) | GOAL (X) | GOAL (X) |
| ✅ GOAL (X) | ✅ GOAL (X) | ✅ GOAL (X) | [GOAL (X)]  [GOAL (X)]  (JJ)  [+] | GOAL (X) | GOAL (X) | GOAL (X) |
|             | ☑️ GOAL (X) | ☑️ GOAL (X) |                                   | GOAL (X) | GOAL (X) |          |
|             | ☑️ GOAL (X) | ☑️ GOAL (X) | ☑️ GOAL (X)                       | GOAL (X) | GOAL (X) |          |
|             | ☑️ GOAL (X) | ✔️ GOAL (X) | ☑️ GOAL (X)                       |          |          |          |
|             | ✔️ GOAL (X) | ✖️ GOAL (X) | ✔️ GOAL (X)                       |          |          |          |
+-------------+-------------+-------------+-----------------------------------+----------+----------+----------+
```

#### Mobile view
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
```





otras variantes:

|  🌻🌻🌻🌻🌻(🌻🌻🌻🌻🌻🌻🌻🌱🌻🌻🌻🌻🌱🌻🌻🥀🌻🌻🌻🌻🌻🌱🌻🌻🌻)🌻🌻🌻 | 👑🪙📝 |
|  🔥🔥🔥🔥🔥(🔥🔥🔥🔥🔥🔥🔥🙂🔥🔥🔥🔥🙂🔥🔥😐🔥🔥🔥🔥🔥🙂🔥🔥🔥)🔥🔥🔥 | 👑🪙📝 |
|  🟩🟩🟩🟩🟩(🟩🟩🟩🟩🟩🟩🟩🟨🟩🟩🟩🟩🟩🟩🟩🟥🟩🟩🟩🟩🟩🟨🟩🟩🟩)🟩🟩🟩 | 👑🪙📝 |
