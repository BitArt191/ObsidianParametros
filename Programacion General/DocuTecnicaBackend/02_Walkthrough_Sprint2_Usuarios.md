---
tags:
  - backend
  - walkthrough
  - sprint2
---

# Sprint 2: Base de Datos de Usuarios y DataSeeder

Este documento registra los cambios implementados para las tareas del Sprint 2 relacionadas con la arquitectura de usuarios y la siembra de datos iniciales.

## Cambios Realizados

1. **Arquitectura de Datos Definida (Composición)**: 
   Decidimos no inflar la tabla genérica `AspNetUsers` (evitando el patrón de Herencia/TPH). En su lugar, creamos entidades especializadas en la capa de datos (`BitArt.Shared/Entities`) para manejar los datos del dominio:
   - `Cliente.cs`: Para clientes (NombreEmpresa, Presupuesto).
   - `Empleado.cs`: Para nuestros trabajadores (Especialidad, Cargo, Salario).
   - `Admin.cs`: Para la gerencia.
   Todas están vinculadas a la identidad a través de un `IdentityUserId` (Relación 1 a 1).

2. **Integración en `ApplicationDbContext`**:
   Se añadieron los `DbSets` correspondientes (`Clientes`, `Empleados`, `Admins`) y se configuró mediante FluentAPI la creación de índices **Únicos (Unique)** sobre el campo `IdentityUserId`. Esto garantiza que a nivel de base de datos SQL un mismo inicio de sesión no pueda tener múltiples perfiles duplicados del mismo rol.

3. **Inyección del Primer Admin (DataSeeder)**:
   Se refactorizó la clase `SeedData.cs`. Ahora, al arrancar el proyecto:
   - Verifica si existe la cuenta `admin@bitart.com`.
   - Si no existe, crea el usuario base en `AspNetUsers` con la contraseña predefinida: `BitArt@Admin2026`.
   - Le asigna el rol `Admin`.
   - Crea automáticamente su registro detallado en la nueva tabla especializada de `Admins`.

## Resultados de Validación
- ✔️ **Compilación**: El proyecto completo (`APPWebBitArt.sln`) se compiló exitosamente.
- ✔️ **GitFlow**: Los cambios se trabajaron aislados en la rama `dev-backend` para asegurar la estabilidad del proyecto.

## Pasos Posteriores para DevOps
Generar y aplicar las migraciones de Entity Framework para que SQL Server cree las nuevas tablas físicas. Es importante usar el flag `--project` para evitar el error "No project was found":
```bash
dotnet ef migrations add AgregarEntidadesDeUsuario --project APPWebBitArt
dotnet ef database update --project APPWebBitArt
```
