---
tags:
  - backend
  - seguridad
  - swagger
---

# Seguridad: Bearer Tokens y Swagger

## 🧠 ¿Qué es un "Bearer" Token?
Cuando usamos JWT (JSON Web Tokens) para proteger nuestra API, el estándar de la industria es enviarlo usando el esquema de autenticación **Bearer**.

La palabra *Bearer* en inglés significa "Portador".
En el mundo real, es como decir: **"Al portador de este billete (token), déjalo entrar."**

A diferencia de otros sistemas de seguridad donde el servidor tiene que buscar en una base de datos quién eres en cada petición, un *Bearer Token* es autosuficiente. El servidor confía ciegamente en quien *porte* el token válido. Si alguien se roba tu token (tu llave), esa persona se convierte en ti para el sistema. Por eso es vital usar HTTPS y tokens que expiren rápido.

### ¿Cómo viaja en una petición HTTP?
Cuando Heidy conecte su Frontend de Blazor a nuestro Backend, ella programará la aplicación para que, en cada petición HTTP, se envíe una cabecera (Header) oculta que se ve exactamente así:
`Authorization: Bearer eyJhbGciOiJIUz...`

## 🛠️ Swagger y la Autorización
Swagger es una herramienta increíble para documentar APIs, pero no sabe mágicamente cómo funciona nuestra seguridad. 

Para que Swagger nos permitiera probar nuestro `AdminController` protegido con `[Authorize(Roles="Admin")]`, tuvimos que:
1. Ir a `Program.cs`.
2. Añadir `AddSecurityDefinition("Bearer", ...)` dentro de la configuración de `AddSwaggerGen()`.
3. Esto obligó a Swagger a mostrar el botón verde de **Authorize** en la interfaz UI.
4. Al poner el token allí, Swagger automáticamente intercepta cada petición que hacemos (como probar el endpoint `POST /api/Admin/create`) y le inyecta el header `Authorization: Bearer <token>` por debajo.

## 🚀 Logros del Día
- Creamos el controlador `AdminController.cs` con el atributo `[Authorize(Roles="Admin")]`.
- Aseguramos que solo un Administrador con un JWT válido pueda crear nuevos administradores.
- Comprobamos el flujo end-to-end exitosamente con Código de Estado HTTP **200 OK**.
