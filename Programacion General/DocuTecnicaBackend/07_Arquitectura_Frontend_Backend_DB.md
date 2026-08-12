---
tags:
  - backend
  - frontend
  - arquitectura
  - seguridad
---

# Arquitectura 3 Capas (Frontend - Backend - Base de Datos)

## 🧠 Concepto Crítico: ¿El Frontend debe conectarse a la Base de Datos?

La respuesta corta y definitiva a nivel corporativo es: **NUNCA**.

Darle acceso directo a la base de datos (SQL Server) a una aplicación Frontend (como Blazor, React, Angular o una app móvil) es la vulnerabilidad de seguridad más grande que puede cometer una empresa. Si el Frontend tiene las contraseñas de la base de datos, cualquier atacante que inspeccione el código de la página web podría robarlas y borrar o robar toda la información de la empresa.

### El Flujo Correcto y Seguro (Arquitectura de 3 Capas)

En un software profesional, se utiliza una arquitectura separada donde el **Backend actúa como un guardia de seguridad (Bouncer) impenetrable**.

1. **Capa 1: Frontend (El Cliente / Heidy)**
   - **Qué hace:** Dibuja la interfaz, los botones y lee la interacción del usuario.
   - **A dónde se conecta:** SOLO puede hablar con el Backend a través de URLs de internet (Endpoints como `https://api.bitart.com/api/Admin/create`).
   - **Cómo habla:** Usando el protocolo HTTP (peticiones GET, POST) e intercambiando archivos JSON.

2. **Capa 2: Backend (La API / Milena)**
   - **Qué hace:** Recibe las peticiones JSON del Frontend, revisa que el usuario tenga permiso (usando los Tokens JWT y `[Authorize]`), valida las reglas de negocio y procesa la información.
   - **A dónde se conecta:** Es el **ÚNICO** que conoce la contraseña secreta de la base de datos (guardada en el `appsettings.json` o en la nube) y el único que puede hablar con ella.

3. **Capa 3: Base de Datos (SQL Server)**
   - **Qué hace:** Almacena los datos de forma segura.
   - **A dónde se conecta:** Acepta conexiones **únicamente** desde la dirección IP del servidor donde está el Backend. Rechaza cualquier conexión directa desde internet o desde el navegador de un cliente.

### Resumen del Flujo de una Petición:
`Usuario hace clic` ➡️ `Frontend (Blazor) envía JSON` ➡️ `Backend (Nuestra API) valida JWT` ➡️ `Backend (Entity Framework) guarda en DB` ➡️ `Backend responde 200 OK` ➡️ `Frontend muestra mensaje de éxito al usuario`.
