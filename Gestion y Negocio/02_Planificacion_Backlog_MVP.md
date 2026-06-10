# 📋 Planificación del MVP y Backlog de Sprints - BITART CORE

Inspirado en la metodología ágil de alto rendimiento (como tu backlog "Camino al Mundial"), estructuramos el desarrollo del MVP de **BitArt Core** en **5 Sprints** de trabajo progresivo. Esto nos permitirá lanzar una primera versión completamente funcional y estable para clientes reales en un tiempo récord.

---

## 🚀 Plan del MVP: 5 Sprints Hacia Producción

```mermaid
gantt
    title Cronograma de Sprints - BitArt Core MVP
    dateFormat  YYYY-MM-DD
    section Desarrollo
    Sprint 1: Base, Seguridad & Config :active, s1, 2026-05-26, 7d
    Sprint 2: Core Loop - Clientes & Proyectos : s2, after s1, 7d
    Sprint 3: Portales de Rol, UI & Calendarios : s3, after s2, 7d
    Sprint 4: Pagos, Integraciones & QA : s4, after s3, 7d
    Sprint 5: Pulido, DevOps & Lanzamiento : s5, after s4, 5d
```

---

### 🏃‍♂️ Sprint 1: Base, Seguridad y Configuración
*   **Enfoque**: Sentar las bases del proyecto, base de datos y flujos de autenticación seguros.
*   **Tareas de Backend (Tus tareas)**:
    *   [x] Configuración de la base de datos SQL Server (`BitArtCoreDB`).
    *   [x] Modelado de la entidad `AccessPin` (pines temporales de acceso).
    *   [x] Implementación de **ASP.NET Core Identity** con roles: `Administrador`, `Empleado` y `Cliente`.
    *   [x] Creación de controladores API para registro e inicio de sesión con **JWT**.
    *   [ ] **(Siguiente Tarea)**: Proyecto de Pruebas Unitarias (`BitArt.Tests`) con tests de robustez para pines de acceso.
*   **Tareas de Frontend (Tu Socia)**:
    *   [x] Diseño responsivo de la Landing Page principal y servicios.
    *   [x] Vistas iniciales de inicio de sesión (`Session.razor`, `Register.razor`).
    *   [x] Configuración y optimización del cargador de modelos 3D (`robotbitart.glb`).

---

### 🏃‍♂️ Sprint 2: Core Loop (Clientes y Proyectos)
*   **Enfoque**: Programar el flujo central del negocio: dar de alta un cliente, asignarle un proyecto y documentar el avance.
*   **Tareas a Desarrollar**:
    *   [ ] **API de Clientes**: Endpoints para CRUD (Crear, Leer, Actualizar, Borrar) de clientes.
    *   [ ] **API de Proyectos**: Endpoints para asignar proyectos a clientes y empleados responsables.
    *   [ ] **Formularios en Frontend**: Pantallas dinámicas del administrador para crear clientes y proyectos de forma amigable (`FormularioCliente.razor`, `FormularioProyecto.razor`).
    *   [ ] **Pruebas**: Pruebas unitarias para validar que un proyecto no pueda crearse sin un cliente real asignado.

---

### 🏃‍♂️ Sprint 3: Portales de Rol y Experiencia de Usuario (UI/UX)
*   **Enfoque**: Separar las experiencias de usuario según su rol (Portal de Admin, Portal de Cliente y Portal de Empleado) y agregar interactividad.
*   **Tareas a Desarrollar**:
    *   [ ] **Panel del Administrador**: Dashboard de control financiero, listados de proyectos y métricas de desempeño.
    *   [ ] **Panel del Cliente**: Vista del cliente para ver el progreso visual de su proyecto de diseño y chatear con su diseñador asignado.
    *   [ ] **Panel del Empleado**: Vista para que el diseñador/desarrollador vea sus tareas pendientes.
    *   [ ] **Calendarios Interactivos**: Implementación y conexión de los calendarios (`CalendarioAdmin.razor`, `Calendario.razor`) con la base de datos para agendar reuniones de avance.

---

### 🏃‍♂️ Sprint 4: Pagos, Integraciones y Aseguramiento de Calidad (QA)
*   **Enfoque**: Integrar pagos reales y asegurar que el sistema sea inmune a fallos lógicos.
*   **Tareas a Desarrollar**:
    *   [ ] **Registro de Pagos**: Implementación de la tabla `Payments` en base de datos.
    *   [ ] **Integración de Pasarela**: Simulación y maquetación de la pasarela de pagos (tarjetas de crédito, transferencias) en el portal de clientes.
    *   [ ] **QA Masivo**: Cobertura del 80% de pruebas unitarias sobre cálculos financieros e historial de pagos.
    *   [ ] **Pruebas de Integración**: Pruebas de API de extremo a extremo (E2E).

---

### 🏃‍♂️ Sprint 5: Pulido, DevOps y Lanzamiento
*   **Enfoque**: Optimizar rendimiento, asegurar infraestructura en la nube y abrir accesos a clientes reales.
*   **Tareas a Desarrollar**:
    *   [ ] **Optimización 3D**: Ajustar el tamaño del archivo `.glb` para que cargue instantáneamente en dispositivos móviles.
    *   [ ] **Despliegue (Deploy)**: Publicación del Servidor e Base de Datos en la nube (ej. Azure o AWS/VPS) y del Frontend WASM en hosting optimizado (ej. Netlify/Vercel o Azure Static Web Apps).
    *   [ ] **Puesta a Punto de Seguridad**: Configurar certificados SSL (HTTPS) y encriptar los secretos de producción.
    *   [ ] **Lanzamiento MVP**: Entrega de los primeros pines de acceso a clientes de prueba.

---

## 📁 Archivos Organizativos Recomendados a Generar en la Bóveda:

Para mantener el proyecto en un estándar corporativo, generaremos los siguientes documentos adicionales en esta carpeta a medida que avancemos:
1.  **`04_Guia_Migraciones_y_BaseDatos.md`**: Un "paso a paso" de cómo alterar la base de datos mediante Entity Framework Core sin perder información.
2.  **`05_Estandar_de_Codigo_Csharp.md`**: Reglas de nombres, uso de CamelCase/PascalCase y arquitectura limpia de archivos para que tu código sea legible y limpio.
3.  **`06_Manual_de_Despliegue_Produccion.md`**: La guía exacta con capturas/instrucciones de cómo subir todo a la nube paso a paso cuando terminemos.
