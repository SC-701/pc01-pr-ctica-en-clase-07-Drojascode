# Autorizacion.Flujo

Lógica de negocio del paquete de autorización. Obtiene los perfiles del usuario
desde la BD y los agrega como `Claim` al `ClaimsPrincipal` activo.
Dependencia interna — consumir a través de `Autorizacion.Middleware`.

- `AutorizacionFlujo` — implementa `IAutorizacionFlujo`
