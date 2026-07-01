---
tags: [project-management, tracker, status]
---

# 📊 Project Manager Tracker - BitArt Core

Este documento actúa como el **Tablero de Control (Dashboard)** del proyecto. Aquí mantendremos las métricas de avance, los tiempos estimados y el porcentaje de completitud de cada fase para tener visibilidad total del esfuerzo del equipo.

## 📈 Estado Global del Proyecto
**Progreso General Estimado:** `45%` 🟩🟩🟩🟩⬜⬜⬜⬜⬜⬜

---

## 🛠️ Desglose por Sprints y Tareas

### Sprint 1: Arquitectura Base y Setup (Completado al 100%)
* **Tiempo Invertido:** ~10 horas.
* **Responsables:** Equipo Fullstack.
* **Estado:** ✅ Completado.
- [x] Configuración de Bóveda Obsidian y Repositorios Git.
- [x] Estructura inicial Clean Architecture (.NET 9 + Blazor).
- [x] Flujo de ramas de DevOps (main, develop, dev-frontend, dev-backend).
- [x] Definición de Backlog y Presupuestos.

### Sprint 2: Frontend UI/UX (Completado al 90%)
* **Tiempo Estimado Original:** 20 horas.
* **Tiempo Invertido:** ~18 horas.
* **Responsables:** Socia Frontend.
* **Estado:** 🟡 En Progreso Final.
- [x] Maquetación de la Landing Page dinámica con CSS y animaciones JS.
- [ ] Ajustes finales de estilo visual y diseño de la Landing Page (Pulido UI) (Viernes).
- [ ]  Ajustes finales de estilo visual perfiles y  revisión de flujo (viernes).
- [x] Integración de carga de modelos 3D (`.glb`).
- [x] Diseño UI Portales (Admin, Cliente, Empleado).
- [ ] Conexión del diseño UI con los datos reales de la API. *(Pendiente Sprint 4)*

### Sprint 3: Backend Security & Integración (Completado al 80%)
* **Tiempo Estimado Original:** 15 horas.
* **Tiempo Restante:** ~3 horas.
* **Responsables:** Backend / IA (Antigravity).
* **Estado:** 🟡 En Progreso (Pruebas pendientes).
- [x] Configuración de SQL Server y Entity Framework Core.
- [x] Implementación de Identity (Autenticación JWT, Usuarios, Roles).
- [x] Controladores de Autenticación y Generación de Pines Secretos.
- [x] Fusión (Merge) exitosa de Frontend y Backend en rama `develop`.
- [x] Migración de variables sensibles a `secrets.json` (DevOps).
- [x] Subir cambios integrados a GitHub (`git push develop`).
- [ ] Implementar Pruebas Unitarias (`BitArt.Tests`) para Auth y Pines.

### Sprint 4: Lógica de Negocio y Conexión (Progreso: 0%)
* **Tiempo Estimado:** 25 horas.
* **Estado:** 🔴 Por Iniciar.
- [ ] Backend: Desarrollar Controladores según los 3 Perfiles (Ej: Pagos para Clientes, Gestión total para Admin).
- [ ] Backend: Desarrollar Controladores de Calendario/Eventos (Visibilidad por Rol).
- [ ] Frontend: Conectar pantalla de Login al JWT real.
- [ ] Frontend: Proteger Rutas en Blazor (Redirección automática según el Rol: Admin, Empleado o Cliente).
- [ ] Frontend: Consumir endpoints de Proyectos, Pagos y Calendario.

---

## ⏳ Resumen de Tiempos
- **Tiempo Total Estimado del MVP:** ~70 Horas.
- **Tiempo Consumido hasta la fecha:** ~31 Horas.
- **Tiempo Restante Estimado:** ~39 Horas.

> [!NOTE] Cita de PM
> *“La base más compleja e invisible del software (arquitectura y seguridad) ya está sólida. El enfoque ahora será interconectar los cables visuales con los datos reales.”*
