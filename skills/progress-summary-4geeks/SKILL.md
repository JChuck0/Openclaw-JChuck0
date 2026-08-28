---
nombre: progress-summary-4geeks
descripción: Proporciona un resumen de avance en 4Geeks Academy: porcentaje completado, distribución por tipo (proyectos, ejercicios, lecciones), y progreso por cohorte activo.
---

## Cuándo Usar
Cuando el usuario quiera saber cómo va su progreso general en el curso, qué porcentaje ha completado, o un resumen de su avance académico.

## Prerrequisitos
- Token de API de BreatheCode en `.env` como `TOKEN_4GEEKS`
- URL base: `https://breathecode.herokuapp.com`

## Endpoints
- `GET /v1/assignment/user/me/task?limit=300` — todas las tareas sin filtrar por estado
- `GET /v1/admissions/user/me` — datos del usuario y cohorts

## Clasificación de estados

| Estado | Progreso |
|---|---|
| `APPROVED` (revision_status) | ✅ Completado |
| `DONE` + `revision_status=PENDING` | 📤 Entregado (esperando revisión) |
| `PENDING` | ⏳ Pendiente |
| `REJECTED` | 🔄 Rehacer |

## Procedimiento
1. Ejecutar `curl -s -H "Authorization: Token ${TOKEN_4GEEKS}" "https://breathecode.herokuapp.com/v1/assignment/user/me/task?limit=300"`.
2. Analizar los resultados:
   a. **Total de tareas asignadas** vs. completadas (APPROVED).
   b. **Por tipo**: desglosar PROJECT, EXERCISE, LESSON, QUIZ en pendientes y completados.
   c. **Por cohorte activo**: agrupar y mostrar avance en cada cohorte.
3. También obtener los datos del usuario (`GET /v1/admissions/user/me`) para listar los cohorts activos.
4. Presentar el resumen:
   - 📊 **Porcentaje global**: "Has completado X de Y tareas totales (Z%)"
   - 📁 **Por tipo**: "Proyectos: X/Y completados | Ejercicios: X/Y | Lecciones: X/Y"
   - 🏫 **Por cohorte**: para cada cohorte activo, cuántas tareas tiene asignadas y cuántas ha completado

## Resultado Esperado
Una visión clara del progreso del estudiante: porcentaje global, desglose por tipo de tarea, y avance por cohorte activo.

## Casos Especiales
- 0 tareas: informar que no hay datos de progreso disponibles.
- Solo un cohorte activo: mostrar el detalle de ese cohorte directamente.
- Error 401: token expiró, sugerir renovarlo.
- Si el usuario pregunta por un cohorte específico, filtrar solo por ese.