---
nombre: pending-work-4geeks
descripción: Muestra el trabajo pendiente de 4Geeks Academy: tareas sin entregar, proyectos pendientes, y entregas esperando revisión, todo organizado por cohorte activo.
---

## Cuándo Usar
Cuando el usuario quiera saber qué le falta por hacer, qué tiene pendiente, o qué entregas están esperando revisión.

## Prerrequisitos
- Token de API de BreatheCode en `.env` como `TOKEN_4GEEKS`
- URL base: `https://breathecode.herokuapp.com`

## Endpoints
- `GET /v1/assignment/user/me/task?task_status=PENDING&limit=100` — tareas pendientes
- `GET /v1/assignment/user/me/task?task_status=DONE&limit=100` — entregadas sin revisar
- `GET /v1/registry/asset/{slug}` — detalle del proyecto/ejercicio (opcional)

## Categorías de trabajo pendiente

| Categoría | Significado |
|---|---|
| 🔴 No empezadas | `task_status=PENDING` — sin entregar |
| 🟡 Pendientes de revisión | `task_status=DONE` con `revision_status=PENDING` |
| 🔵 Proyectos activos | Proyectos (`task_type=PROJECT`) del cohorte activo que siguen PENDING |

## Procedimiento

### Para obtener una visión general del trabajo pendiente
1. Ejecutar `curl -s -H "Authorization: Token ${TOKEN_4GEEKS}" "https://breathecode.herokuapp.com/v1/assignment/user/me/task?task_status=PENDING&limit=100"`.
2. Ejecutar `curl -s -H "Authorization: Token ${TOKEN_4GEEKS}" "https://breathecode.herokuapp.com/v1/assignment/user/me/task?task_status=DONE&limit=100"`.
3. Analizar los resultados:
   a. De las tareas PENDING: agrupar por cohorte y por tipo (PROJECT, EXERCISE, LESSON, QUIZ).
   b. De las tareas DONE: filtrar aquellas con `revision_status=PENDING` (entregadas pero sin revisar).
4. Mostrar un resumen con:
   - Total de tareas pendientes por cohorte activo
   - Desglose por tipo (proyectos, ejercicios, lecciones)
   - Cuántas entregas están esperando revisión

### Para ver detalle de un proyecto pendiente específico
1. Identificar el proyecto por título o `associated_slug` de la lista PENDING.
2. Ejecutar `curl -s -H "Authorization: Token ${TOKEN_4GEEKS}" "https://breathecode.herokuapp.com/v1/registry/asset/{slug}"`.
3. Mostrar: título, descripción, dificultad, tecnologías requeridas.

## Resultado Esperado
El agente devuelve una visión clara de todo el trabajo pendiente: tareas sin empezar agrupadas por cohorte y tipo, más las entregas pendientes de revisión. Si se pide detalle de algo concreto, lo amplía.

## Casos Especiales
- Sin trabajo pendiente: felicitar al usuario, está al día.
- Sin entregas pendientes de revisión: indicar que no hay nada esperando.
- Error 401: token expiró, sugerir renovarlo.
- El usuario puede filtrar por cohorte si solo le interesa uno en concreto.