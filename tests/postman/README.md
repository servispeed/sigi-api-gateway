# Pruebas de integración (Postman)
Flujo: **API Gateway → Security → Personas → MQTT → Notifications**.

## Archivos incluidos
* `sigi-http-tests.json`: Colección con peticiones HTTP (Login y Disparador de eventos).
* `sigi-env.json`: Entorno con las variables base.

## Cómo ejecutar la prueba completa

1. **Importar y Configurar:**
   * Importa ambos archivos `.json` en Postman.
   * Selecciona el entorno `SIGI Prod` y coloca tus credenciales en el Body del Login.

2. **Paso 1: Autenticación**
   * Ejecuta `1. Login (Security)`. El JWT se guardará automáticamente en tu entorno.

3. **Paso 2: Conexión websocket**
   * En Postman, crea un **New > WebSocket Request**.
   * URL: `{{ws_url}}` (ej. `ws://74.208.123.250/ws/`).
   * En **Message**, envía este JSON para registrar tu sesión:
```json
{
  "type": "INIT_SESSION",
  "userId": "16"
}
```
   * **Mantén esta pestaña abierta.**

4. **Paso 3: Disparar el evento**
* Vuelve a la colección HTTP y ejecuta `3. Launch event (Notifications)`.
* Revisa tu pestaña de WebSocket. Si hay eventos que emitan notificaciones, las verás llegar en tiempo real.