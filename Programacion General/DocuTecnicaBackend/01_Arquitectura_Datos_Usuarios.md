---
tags:
  - backend
  - arquitectura
  - database
---

# Arquitectura de Datos de Usuarios

## 🧠 Concepto Crítico para Milena: Herencia vs Composición en Bases de Datos

Como desarrolladora y arquitecta de software, una de las decisiones más importantes que tomarás es cómo diseñar la base de datos cuando tienes diferentes tipos de usuarios (ej. Clientes, Empleados, Administradores).

### El Problema
ASP.NET Core Identity nos da una tabla genérica llamada `AspNetUsers` (representada por la clase `IdentityUser`). Pero un **Cliente** tiene datos como `Presupuesto` o `NombreEmpresa`, mientras que un **Empleado** tiene `Especialidad` o `Salario`. ¿Dónde guardamos esos datos?

### Opción 1: Herencia (TPH - Table Per Hierarchy)
Consiste en meter **absolutamente todos** los campos posibles en la misma tabla `AspNetUsers`. 
- **Ventaja**: Las consultas son muy rápidas (solo lees una tabla).
- **Desventaja (Por qué no la elegimos)**: Si un Cliente no tiene "Salario", ese campo quedará en `NULL`. A medida que el sistema crece, tu tabla terminará teniendo 100 columnas, de las cuales 80 siempre estarán vacías dependiendo del tipo de usuario. Esto se vuelve inmanejable.

### Opción 2: Composición (Tablas Separadas - La Elección de BitArt)
Mantenemos la tabla `AspNetUsers` limpia, usándola **solo para la autenticación** (Email, Password Hash, etc.). Luego, creamos tablas separadas (`Clientes`, `Empleados`, `Admins`) que tienen una relación 1 a 1 mediante una Clave Foránea (Foreign Key) apuntando al Id del usuario.
- **Ventaja**: Cumple con el Principio de Responsabilidad Única (SOLID). Las tablas son pequeñas, limpias y ordenadas. Cada entidad tiene solo los datos que le corresponden.
- **Lección como Desarrolladora**: En sistemas corporativos reales que van a escalar (como BitArt), **siempre** debes preferir la composición o normalización de tablas sobre bases de datos "monstruo" llenas de nulos, a menos que el rendimiento sea un cuello de botella tan extremo que justifique desnormalizar.

---

## 🏗️ Implementación en BitArt Core (Sprint 2)

Las entidades se han diseñado de la siguiente manera usando Entity Framework Core:

1.  **IdentityUser**: Maneja el login.
2.  **Cliente**: Contiene `IdentityUserId` (FK). Almacena los datos del cliente.
3.  **Empleado**: Contiene `IdentityUserId` (FK). Almacena los datos del diseñador/dev.
4.  **Admin**: Contiene `IdentityUserId` (FK). Almacena datos gerenciales.

*(Esta documentación está viva y se actualizará a medida que Nova y Milena expandan el sistema).*
