# Autorizacion.DA

Capa de acceso a datos del paquete de autorización. Consulta los perfiles (roles)
asignados a un usuario en la BD de seguridad usando Dapper.
Dependencia interna — consumir a través de `Autorizacion.Middleware`.

- `SeguridadDA` — implementa `ISeguridadDA`
- `RepositorioDapper` — ejecuta las consultas SQL
