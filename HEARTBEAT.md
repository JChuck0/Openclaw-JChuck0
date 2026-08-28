<!-- Heartbeat template; comments-only content prevents scheduled heartbeat API calls. -->

# Keep this file empty (or with only comments) to skip heartbeat API calls.

# Add tasks below when you want the agent to check something periodically.

## Revisión diaria del calendario de clases

En cada ciclo de heartbeat:
1. Comprueba la hora actual. Si todavía no son las 8:00, no hagas nada.
2. Lee `memory/heartbeat-state.json` (créalo con `lastChecks: {}` si no existe) y mira el valor de `lastChecks.calendar`.
3. Si `lastChecks.calendar` ya corresponde a la fecha de hoy, no hagas nada — ya se ejecutó.
4. Si no corresponde a hoy (o no existe), ejecuta la skill `revisar-calendario-clases` y actualiza `lastChecks.calendar` con la fecha/hora actual.