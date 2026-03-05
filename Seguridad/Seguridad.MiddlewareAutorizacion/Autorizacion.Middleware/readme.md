# Autorizacion.Middleware

Middleware de ASP.NET Core 8 que consulta los perfiles (roles) del usuario
autenticado en la base de datos de seguridad y los agrega como `Claim`
al `HttpContext.User`.

## Instalación

```bash
dotnet add package Autorizacion.Middleware --version 2.0.6 \
  --source "https://nuget.pkg.github.com/Drojascode/index.json"
```

## Configuración en `Program.cs`

```csharp
// 1. Registrar los servicios en el DI container
builder.Services.AddTransient<IAutorizacionFlujo, AutorizacionFlujo>();
builder.Services.AddTransient<ISeguridadDA, SeguridadDA>();
builder.Services.AddTransient<IRepositorioDapper, RepositorioDapper>();

// 2. Agregar al pipeline (el orden es OBLIGATORIO)
app.UseAuthentication();    // lee la cookie / Bearer → llena HttpContext.User
app.AutorizacionClaims();   // ← este middleware: agrega claims de rol desde BD
app.UseAuthorization();     // verifica [Authorize(Roles = "1")]
```

## Requisitos

- .NET 8
- `ConnectionStrings:BD` en `appsettings.json` apuntando a la BD de seguridad
- Tablas `Usuarios`, `Perfiles` y `UsuariosPerfiles` existentes en la BD

## Dependencias

- `Autorizacion.Abstracciones` — interfaces y modelos compartidos
- `Autorizacion.DA` — acceso a la BD de seguridad (Dapper)
- `Autorizacion.Flujo` — lógica que arma los claims
