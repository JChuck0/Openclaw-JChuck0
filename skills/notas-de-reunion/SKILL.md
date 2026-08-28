---
nombre: notas-de-reunion
descripción: Convierte apuntes en bruto de una reunión en una nota estructurada (decisiones, tareas, preguntas abiertas) y la guarda como documento en Google Drive.
---

## Cuándo Usar
Se activa cuando el usuario pega el texto en bruto de una reunión y pide explícitamente que se estructure y se guarde.

## Prerrequisitos
- Conexión activa a Google Drive (vía Zapier)
- Nombre de la carpeta de Drive donde se guardan las notas (ajusta esto a tu propia estructura, por ejemplo "Notas de reuniones")
- Texto en bruto de la reunión, proporcionado por el usuario en el mismo mensaje que activa la skill

## Procedimiento
1. Leer el texto en bruto de la reunión que el usuario ha pegado.
2. Extraer del texto las decisiones tomadas y listarlas bajo un apartado "Decisiones".
3. Extraer las tareas o acciones pendientes mencionadas y listarlas bajo un apartado "Tareas".
4. Extraer las preguntas o puntos sin resolver mencionados y listarlas bajo un apartado "Preguntas abiertas".
5. Crear un nuevo documento en la carpeta de Drive indicada, con título que incluya la fecha de hoy, y las tres secciones anteriores.
6. Confirmar al usuario que el documento se creó, indicando su nombre.

## Resultado Esperado
Existe un nuevo documento en Drive con las tres secciones (Decisiones, Tareas, Preguntas abiertas) rellenas según lo mencionado en el texto pegado, y el usuario recibe confirmación con el nombre del documento.

## Casos Especiales
- Si el texto pegado no menciona nada en una de las tres categorías (por ejemplo, no hay preguntas abiertas), esa sección se crea igualmente mostrando "Ninguna" en vez de omitirse.
- Si el texto pegado está vacío o no parece contener contenido de una reunión, el agente lo indica al usuario y no crea ningún documento.
- Si falla la conexión con Google Drive, se informa al usuario del motivo exacto del fallo, sin intentar guardar en otro sitio silenciosamente.
