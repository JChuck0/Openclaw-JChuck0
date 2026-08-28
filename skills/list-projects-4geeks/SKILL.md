---
nombre: list-projects-4geeks
descripción: Obtiene los proyectos de 4Geeks Academy, los clasifica en pendientes, entregados y calificados, y devuelve el estado. Si se pide, muestra el resumen/descripción de los pendientes.
---

## Cuándo Usar
Cuando el usuario quiera ver sus proyectos de 4Geeks, su estado, o los detalles de los que están pendientes.

## Prerrequisitos
- Token de API de BreatheCode en `.env` como `TOKEN_4GEEKS`
- URL base: `https://breathecode.herokuapp.com`

## Endpoints utilizados
- `GET /v1/assignment/user/me/task?task_type=PROJECT&limit=100` — lista de proyectos
- `GET /v1/registry/asset/{associated_slug}` — descripción detallada del proyecto (cuando se pida)

## Clasificación de estados

| Estado API | Clasificación | Descripción |
|---|---|---|
| `PENDING` | 🔴 Pendiente | No entregado aún |
| `DONE` | 🟡 Entregado | Entregado, esperando revisión |
| `APPROVED` (revision_status) | 🟢 Calificado | Aprobado con feedback |
| `REJECTED` (revision_status) | 🔴 Rechazado | Requiere correcciones |

## Procedimiento

### Si el usuario pide lista de proyectos
1. Ejecutar `curl -s -H "Authorization: Token ${TOKEN_4GEEKS}" "https://breathecode.herokuapp.com/v1/assignment/user/me/task?task_type=PROJECT&limit=100"`.
2. Agrupar los resultados por `task_status`:
   - `PENDING` → Pendientes
   - `DONE` → Entregados
   - `APPROVED` / `REJECTED` (según `revision_status`) → Calificados / Rechazados
3. Mostrar un resumen con el conteo de cada categoría.
4. Listar los proyectos de cada categoría con: título, cohorte, y estado.

### Si el usuario pide descripción de un proyecto pendiente
1. Obtener la lista de proyectos pendientes (como en el paso 1).
2. Identificar el proyecto por título o `associated_slug`.
3. Ejecutar `curl -s -H "Authorization: Token ${TOKEN_4GEEKS}" "https://breathecode.herokuapp.com/v1/registry/asset/{associated_slug}"`.
4. Mostrar: título, descripción completa, dificultad, tecnologías.

### Si el usuario pide solo el estado de un proyecto concreto
1. Buscar el proyecto por título en la lista completa.
2. Devolver: título, estado, y cohorte.

## Resultado Esperado
El agente devuelve los proyectos organizados por estado (pendiente/entregado/calificado) con conteos. Si se pide detalle de uno pendiente, muestra la descripción del asset. Si solo se pide estado, devuelve el estado sin más detalles.

## Casos Especiales
- Sin proyectos: informar que no hay proyectos asignados.
- Proyecto no encontrado: indicar que no existe con ese nombre.
- Error 401: el token expiró, sugerir renovarlo.
- Varios proyectos con mismo nombre: usar el `associated_slug` para identificar el correcto.