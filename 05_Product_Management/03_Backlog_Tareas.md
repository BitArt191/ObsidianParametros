# Backlog de Tareas

## Leyenda de Etiquetas
**Estados:**
- `#task`: Tarea general
- `#in-progress`: Tarea en curso
- `#high-priority`: Prioridad alta
- `#completed`: Tarea finalizada

**Áreas de Responsabilidad:**
- `#backend`: Lógica de negocio, APIs, controladores (Milena)
- `#data`: Modelos, SQL, Entity Framework (Milena)
- `#devops`: GitFlow, CI/CD, Azure/AWS, Tests (Milena)
- `#frontend`: Blazor, CSS, UI/UX, Modelos 3D (Heidy)

## Sprint 1: Base, Seguridad y Configuración (Completado)
- [x] Configuración de base de datos SQL Server y Entity Framework `#data` `#completed`
- [x] Modelado de entidad AccessPin y Identity `#backend` `#data` `#completed`
- [x] Sincronización GitFlow (Develop) y Frontend Base `#devops` `#frontend` `#completed`
- [x] Pruebas Unitarias para AccessPin (xUnit) `#devops` `#completed`
- [x] Integración Continua CI/CD con GitHub Actions `#devops` `#completed`

## Sprint 2: Core Loop (Usuarios, Clientes y Proyectos)
- [ ] Data Seeding y Gestión de Administradores `#backend` `#data` `#frontend` #in-progress 🔺 📅 2026-07-28
  - [x] **Milena (Data)**: Crear un `DataSeeder` (Sembrador de datos) para inyectar automáticamente el Primer Admin (Root) al arrancar la app.
  - [x] **Milena (Backend)**: Crear endpoint restringido `[Authorize(Roles="Admin")]` para permitir crear otros administradores.
  - [x] **Heidy (Frontend)**: Crear `FormularioAdmin.razor` (interfaz exclusiva para administradores) que consuma el endpoint protegido. ✅ 2026-08-18
- [ ] API de Perfiles: Clientes, Empleados y Admins (CRUD) `#backend` `#data` 🔽 📅 2026-07-31
  - [x] **Milena (Data)**: Crear las entidades `Cliente`, `Empleado` y `Admin` (o una tabla unificada con Roles) en `BitArt.Shared`.
  - [x] **Milena (Data)**: Añadir `DbSet` para los perfiles en `ApplicationDbContext` y generar Migración.
  - [x] **Milena (Backend)**: Crear patrón Repositorio genérico o específico para los perfiles.
  - [ ] **Milena (Backend)**: Crear controladores (`ClientesController`, `EmpleadosController`, etc.) con endpoints GET, PUT, DELETE.
- [ ] API de Proyectos y Asignación `#backend` `#data` 🔽 📅 2026-08-05
  - [ ] **Milena (Data)**: Crear entidad `Proyecto` con llaves foráneas para `Cliente` (One-to-Many) y `Empleado` (Many-to-Many o One-to-Many según decidan).
  - [ ] **Milena (Data)**: Generar migración de EF Core para reflejar las relaciones en SQL Server.
  - [ ] **Milena (Backend)**: Crear `ProyectosController` con endpoints CRUD básicos.
  - [ ] **Milena (Backend)**: Crear endpoint especializado para "Asignar Proyecto" a un Cliente o Empleado.
- [ ] Admin: Formularios de creación de Perfiles (`FormularioCliente.razor` y `FormularioEmpleado.razor`) `#frontend`
  - [ ] Crear clases `ClienteFormDTO` y `EmpleadoFormDTO` con anotaciones.
  - [ ] Implementar `<EditForm>` con validaciones para crear tanto Clientes como Empleados.
  - [ ] Añadir `<ValidationMessage>` y manejar los estados de carga.
- [ ] Admin: Formulario de creación de Proyectos (`FormularioProyecto.razor` - Validaciones y estado) `#frontend`
  - [ ] Replicar la misma lógica de `EditForm` y validaciones estructuradas.
- [ ] Pruebas unitarias de integridad de relaciones de perfiles y proyectos `#devops`
- [ ] Integración API Frontend-Backend en los formularios de Admin `#frontend` `#backend`
  - [ ] **Milena (Backend)**: Crear endpoints `POST` para registrar Clientes y Empleados.
  - [ ] **Milena (Backend)**: Validar DTOs, asignar los roles correspondientes (Identity) y guardar en base de datos.
  - [ ] **Milena (Backend)**: Retornar HTTP 201 (Éxito) o HTTP 400 (Errores).
  - [ ] **Heidy (Frontend)**: Inyectar `HttpClient` en Blazor y enviar los DTOs correspondientes.
  - [ ] **Heidy (Frontend)**: Mostrar alertas globales o pantallas de éxito dependiendo del perfil creado.

## Sprint 3: Portales de Rol y Experiencia de Usuario (UI/UX)
- [ ] Dashboard Admin: Conectar `Finanzas.razor` y KPIs con datos reales `#frontend` `#backend`
  - [ ] **Milena (Backend)**: Crear endpoint `GET /api/dashboard/admin/kpis` que calcule ingresos, clientes totales y proyectos activos consultando Entity Framework.
  - [ ] **Heidy/Milena (Frontend)**: Consumir el endpoint mediante `HttpClient` y mapear los datos a las tarjetas y gráficos estáticos de `Finanzas.razor`.
- [ ] Dashboard Admin: Implementar interactividad en `CalendarioAdmin.razor` `#frontend`
  - [ ] **Milena (Backend)**: Crear endpoint `GET /api/dashboard/admin/calendario` que retorne las fechas límite de proyectos y reuniones.
  - [ ] **Heidy/Milena (Frontend)**: Inyectar los eventos reales obtenidos de la API en la grilla interactiva del calendario.
- [ ] Dashboard Cliente: Conectar `Proyectos.razor` con base de datos `#frontend` `#backend`
  - [ ] **Milena (Backend)**: Crear endpoint `GET /api/dashboard/cliente/proyectos` estrictamente filtrado por el ID del usuario logueado (Identity).
  - [ ] **Heidy/Milena (Frontend)**: Reemplazar las tablas estáticas en `Proyectos.razor` por un foreach que itere los proyectos reales del cliente.
- [ ] Dashboard Empleado: Conectar `DashboardEmp.razor` con tareas asignadas `#frontend` `#backend`
  - [ ] **Milena (Backend)**: Crear endpoint `GET /api/dashboard/empleado/tareas` filtrado por el empleado autenticado.
  - [ ] **Heidy/Milena (Frontend)**: Renderizar la lista de tareas pendientes, en curso y finalizadas del empleado.
- [ ] Implementar `AuthorizeView` y control de roles en todas las vistas `#frontend` `#backend`
  - [ ] **Milena (Backend)**: Auditar que todos los endpoints de la API estén protegidos con su respectivo `[Authorize(Roles="...")]`.
  - [ ] **Heidy/Milena (Frontend)**: Envolver los componentes de navegación (Sidebar, Header) y páginas en `<AuthorizeView>` de Blazor para ocultar menús a roles no autorizados.

## Sprint 4: Pagos, Integraciones y Aseguramiento de Calidad (QA)
- [ ] Entidad Payment y API `#backend` `#data`
  - [ ] **Milena (Data)**: Crear entidad `Pago` en `BitArt.Shared` con relación al `Proyecto` y al `Cliente` (guardando monto, fecha, estado y referencia externa).
  - [ ] **Milena (Data)**: Añadir `DbSet<Pago>`, configurar relaciones en `ApplicationDbContext` y crear la Migración.
  - [ ] **Milena (Backend)**: Crear `PagosController` para generar intenciones de pago (Checkout).
  - [ ] **Milena (Backend)**: Implementar Webhooks seguros para recibir confirmación asíncrona de la pasarela (ej. Stripe, PayPal o MercadoPago).
- [ ] UI de Pasarela de Pagos (Vista Cliente) `#frontend`
  - [ ] **Heidy (Frontend)**: Integrar el SDK/Checkout de la pasarela seleccionada en la vista `Pagos.razor` del portal del Cliente.
  - [ ] **Heidy (Frontend)**: Crear las vistas de respuesta (Pago Exitoso / Pago Rechazado / Pendiente).
  - [ ] **Heidy/Milena (Frontend)**: Conectar el botón de pagar con la API para iniciar la transacción de forma segura.
- [ ] Gestión Financiera (Vista Admin) `#frontend` `#backend`
  - [ ] **Milena (Backend)**: Crear endpoint `GET /api/pagos/admin` para consultar el historial financiero global (filtrable por fechas, clientes y estado).
  - [ ] **Heidy (Frontend)**: Conectar `PagosAdmin.razor` con la API para mostrar la tabla de todos los ingresos de la empresa.
- [ ] Cobertura 80% pruebas unitarias `#devops`
  - [ ] **Milena (DevOps)**: Escribir pruebas unitarias con `xUnit` y `Moq` para todos los Controllers (`Clientes`, `Proyectos`, `Pagos`).
  - [ ] **Milena (DevOps)**: Configurar *Coverlet* (herramienta de cobertura) para medir qué porcentaje del backend está testeado.
  - [ ] **Milena (DevOps)**: Configurar GitHub Actions para que rechace (falle) cualquier Pull Request que baje la cobertura del 80%.

## Sprint 5: Pulido, DevOps y Lanzamiento a Producción
- [ ] Pulido de UI, Landing Page y 3D `#frontend`
  - [ ] **Heidy (Frontend)**: Ajustar responsive design (móvil y tablet), animaciones y links muertos en la Landing Page.
  - [ ] **Heidy (Frontend)**: Optimizar la carga del modelo 3D `.glb` (compresión y pre-carga) para que no afecte el rendimiento web.
- [ ] Refactorización y Limpieza de Código `#frontend` `#backend`
  - [ ] **Heidy (Frontend)**: Limpiar CSS y extraer clases muy largas de Tailwind a componentes reutilizables en Blazor.
  - [ ] **Milena (Backend)**: Eliminar código muerto (comentado), resolver *Warnings* del compilador y limpiar los logs del servidor.
- [ ] Despliegue en Producción (Versión 1.0) `#devops`
  - [ ] **Milena (DevOps)**: Desplegar y asegurar la base de datos SQL Server definitiva en la nube (ej. Azure SQL).
  - [ ] **Milena (DevOps)**: Configurar el servicio de alojamiento web (ej. Azure App Service o Contenedores Docker).
  - [ ] **Milena (DevOps)**: Inyectar variables de entorno de producción (cadenas de conexión reales) como *Secrets* en GitHub Actions para que los pases a producción sean automáticos.

## 💡 Documentación Técnica Pendiente (A generar a futuro)
*Estos manuales surgieron de la planificación del MVP y se irán creando conforme avance el proyecto.*
- [ ] **PM:** Crear `06_Guia_Migraciones_y_BaseDatos.md`: Un "paso a paso" de cómo alterar la base de datos mediante Entity Framework Core en equipo.
- [ ] **PM:** Crear `07_Estandar_de_Codigo_Csharp.md`: Reglas de nombres, uso de CamelCase/PascalCase y arquitectura limpia.
- [ ] **PM:** Crear `08_Manual_de_Despliegue_Produccion.md`: La guía exacta con capturas e instrucciones de cómo subir todo a la nube (para el Sprint 5).
