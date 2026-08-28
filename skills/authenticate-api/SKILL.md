---
nombre: authenticate-api
descripción: Skill genérica de autenticación de APIs. Verifica que un token almacenado en .env es válido y que la sesión del API está activa.
---

## Cuándo Usar
Cuando el usuario conecte una nueva API y guarde su token en `.env`, o cuando pida verificar que una API sigue funcionando correctamente.

## Prerrequisitos
- Token del API guardado en `/root/.openclaw/.env` con el nombre de variable especificado (ej. `TOKEN_4GEEKS`, `TOKEN_GITHUB`, etc.)
- Conocimiento de la URL base y endpoint de autenticación del API
- Preferiblemente usar `curl` para peticiones HTTP con cabeceras personalizadas

## Registro de APIs conocidas

| API | Nombre variable | URL base | Endpoint auth | Formato Auth |
|---|---|---|---|---|
| 4Geeks / BreatheCode | TOKEN_4GEEKS | https://breathecode.herokuapp.com | GET /v1/admissions/user/me | Token ${TOKEN} |
| *(ampliable según se conecten nuevas APIs)* | | | | |

## Procedimiento
1. Identificar qué API se quiere verificar (por nombre o por variable de entorno).
2. Si el API está en el registro conocido, usar sus datos (URL base, endpoint, formato de auth).
3. Si no está registrada, solicitar al usuario: URL base, endpoint de verificación, y formato de la cabecera Authorization.
4. Ejecutar `curl -s -H "Authorization: <formato>" <url_base><endpoint>` usando el token del `.env`.
5. Si la respuesta es 200 OK y contiene datos del usuario/sesión, informar que el token es válido y la sesión está activa, mostrando los datos relevantes (email, nombre, etc.).
6. Si la respuesta es 401, informar que el token ha expirado o es inválido, y sugerir renovarlo.
7. Si hay error de red o DNS, informar del error sin mostrar datos sensibles.

## Resultado Esperado
El agente confirma que el token del API es válido y la sesión está activa, mostrando datos básicos de la cuenta. Si no es válido, informa del error y sugiere renovar el token.

## Casos Especiales
- Token vacío o no configurado en `.env`: informar al usuario y sugerir añadirlo.
- API no registrada: pedir al usuario la URL base, endpoint y formato de auth.
- Error 401: el token expiró. Sugerir renovarlo en la plataforma correspondiente.
- Error de red/DNS: mostrar el error técnico sin datos sensibles.
- Múltiples APIs: si el usuario no especifica cuál, listar las disponibles en `.env` y preguntar.