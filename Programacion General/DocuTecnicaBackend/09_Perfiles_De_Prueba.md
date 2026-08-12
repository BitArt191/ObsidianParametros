---
tags:
  - backend
  - qa
  - testing
  - credenciales
---

# Perfiles de Prueba (Entorno de Desarrollo)

Para mantener un registro de las cuentas creadas durante nuestras sesiones de QA (Quality Assurance), aquí documentamos los perfiles que existen actualmente en la base de datos local para realizar pruebas en Swagger y en el Frontend.

## 1. Administradores (Acceso Total)

**Perfil 1: Admin Principal**
- **Email:** `admin@bitart.com`
- **Password:** `BitArt@Admin2026`
- **Rol:** Admin
- *Uso:* Utilizar este usuario para loguearse en `/api/Auth/login`, obtener el Token JWT y tener permisos para crear Clientes, Empleados y gestionar todo el sistema.

## 2. Clientes (Acceso de Cliente)

**Perfil 1: Cliente de Prueba (SpaceX)**
- **Email:** `nuevo.cliente@gmail.com`
- **Password:** `PasswordSeguro123!`
- **Rol:** Cliente
- **Representante:** Elon Musk
- **Empresa:** SpaceX
- **Sector:** Aeroespacial
- *Uso:* Utilizar para probar flujos donde el cliente inicia sesión para ver sus proyectos asignados.

## 3. Empleados (Acceso Operativo)

**Perfil 1: Empleado de Prueba (Backend)**
- **Email:** `dev.backend@bitart.com` *(Pendiente por crear en QA)*
- **Password:** `DevBackend2026!`
- **Rol:** Empleado
- **Nombre:** Heidy Desarrolladora
- **Especialidad:** Backend
- *Uso:* Utilizar para probar la asignación de empleados a los proyectos.
