---
nombre: authenticate-4geeks
descripción: Verifica que el token de la API de BreatheCode/4Geeks Academy es válido consultando el endpoint de usuario actual.
---

## Cuándo Usar
Cuando el usuario pida verificar su token de 4Geeks, autenticar su sesión, o comprobar que la integración con la API de BreatheCode funciona correctamente.

## Prerrequisitos
- Token de API de BreatheCode en `.env` como `TOKEN_4GEEKS`
- URL base por defecto: `https://breathecode.herokuapp.com`

## Procedimiento
1. Ejecutar: `curl -s -H "Authorization: Token ${TOKEN_4GEEKS}" https://breathecode.herokuapp.com/v1/admissions/user/me`
2. Si la respuesta incluye un email y nombre de usuario, mostrar los datos básicos como confirmación de que el token es válido.
3. Si la respuesta es un 401, informar al usuario de que el token no es válido o ha expirado, y sugerir renovarlo en la plataforma de 4Geeks.
4. Si hay otro error (red, DNS, etc.), mostrar el mensaje de error sin datos sensibles.

## Resultado Esperado
El agente confirma si el token es válido mostrando los datos básicos del usuario (email, nombre), o informa del error con una sugerencia clara si no lo es.

## Casos Especiales
- Token vacío o no configurado en `.env`: informar al usuario y pedir que lo añada.
- Error 401: el token expiró o es inválido. Sugerir renovarlo.
- La URL base puede variar según el entorno; si el usuario lo indica, usarla en lugar de la default.