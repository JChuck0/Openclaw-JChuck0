---
nombre: revisar-calendario-clases
descripción: Revisa el calendario "Clases 4Geeks" y, si hay clase ese día, avisa por Telegram con el nombre de la clase.
---

## Cuándo Usar
Se activa cuando HEARTBEAT.md indica, en su ciclo diario, que toca revisar el calendario de clases.

## Prerrequisitos
- Conexión activa a Google Calendar.
- Nombre exacto del calendario a consultar: "Clases 4Geeks"
- Token de bot de Telegram en .env, referenciado como ${TELEGRAM_BOT_TOKEN} en openclaw.json
- ID del chat de Telegram al que enviar el aviso

## Procedimiento
1. Usar la conexión a Google Calendar para listar los eventos del calendario "Clases 4Geeks" en la fecha de hoy.
2. Si no hay ningún evento, terminar sin enviar mensaje.
3. Si hay exactamente un evento, tomar su nombre y quitar cualquier texto entre paréntesis.
4. Si hay más de un evento, tomar el primero por hora de inicio y registrar en los logs del espacio de trabajo que hubo varios eventos ese día.
5. Enviar por Telegram: "Carlos, hoy tienes clase de {nombre de la clase sin paréntesis}!"

## Resultado Esperado
Los días con clase, llega el mensaje de Telegram con el nombre correcto antes de que empiece el día. Los días sin clase, no llega ningún mensaje — eso también cuenta como éxito, no como fallo.

## Casos Especiales
- Sin eventos ese día: comportamiento normal, no se envía nada.
- Más de un evento ese día: se usa el primero por hora y se deja constancia en los logs.
- Fallo de conexión con el calendario o con Telegram: se registra la causa exacta en los logs del espacio de trabajo, y si Telegram sigue accesible, se avisa con "Error al revisar el calendario: {causa}" — sin pasar por `openclaw doctor`.




---
nombre: notas-de-reunion
descripción: Convierte apuntes en bruto de una reunión en una nota estructurada (decisiones, tareas, preguntas abiertas) y la guarda como documento en Google Drive.
---

## Cuándo Usar
Se activa cuando el usuario pega el texto en bruto de una reunión y pide explícitamente que se estructure y se guarde.

## Prerrequisitos
- Conexión activa a Google Drive (vía Composio)
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