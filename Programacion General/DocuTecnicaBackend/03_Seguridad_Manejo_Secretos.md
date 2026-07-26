---
tags:
  - backend
  - seguridad
  - devops
---

# Seguridad y Manejo de Secretos

## 🧠 Concepto Crítico para Milena: ¿Por qué NUNCA debemos "quemar" (Hardcode) credenciales en el código fuente?

Cuando estamos desarrollando un MVP rápido, a menudo es tentador inicializar variables importantes directamente en el archivo `.cs`:
```csharp
// ❌ ESTO ES UNA VULNERABILIDAD CRÍTICA
var passwordAdmin = "BitArt@Admin2026";
await userManager.CreateAsync(adminUser, passwordAdmin);
```

### ¿Cuál es el peligro real?
1. **Fugas en el Control de Versiones (Git)**: Si subimos ese código a GitHub, GitLab o Bitbucket, cualquier persona con acceso al repositorio (incluso un empleado que ya no trabaja contigo) puede leer la contraseña del administrador general del sistema.
2. **Inflexibilidad en Despliegues**: Si quieres tener una contraseña diferente para tu servidor de Pruebas (Staging) y otra para Producción, tendrías que ir, cambiar el código, volver a compilar y volver a subir todo. Eso rompe con la integración continua (CI/CD).

### La Solución Corporativa: IConfiguration y Archivos Externos
ASP.NET Core está diseñado desde cero con un patrón llamado **Options Pattern** y una interfaz **`IConfiguration`**. 

En lugar de escribir la contraseña, le pedimos al sistema que busque una "llave" específica:
```csharp
// ✔️ ESTA ES LA MANERA PROFESIONAL
var adminPassword = configuration["AdminDefaultSettings:Password"];
```

¿Dónde busca `IConfiguration` esa llave?
ASP.NET Core la busca en múltiples capas (en este orden específico):
1. Archivo `appsettings.json` (Ideal para desarrollo local).
2. Secrets Manager local (Ideal para desarrollo sin tocar archivos que se van a GitHub).
3. Variables de Entorno del Sistema Operativo (Ideal para contenedores Docker o Linux).
4. Proveedores de Nube (Azure Key Vault o AWS Secrets Manager - Estándar para Producción).

### Lección DevOps
Cuando BitArt Core salga a producción, nuestro código `SeedData.cs` será exactamente el mismo. Pero en el servidor de Azure o AWS, simplemente configuraremos una variable de entorno segura (que solo tú puedes ver) llamada `AdminDefaultSettings__Password` con la contraseña real. Nuestro backend la leerá mágicamente sin arriesgar la seguridad.
