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
