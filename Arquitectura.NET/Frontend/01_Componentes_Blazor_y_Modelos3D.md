# 🎨 Componentes Blazor, Hojas de Estilo y Visualización 3D - FRONTEND

Este documento detalla la estructura visual y técnica del frontend de **BitArt Core**, la organización de los componentes interactivos de Blazor WebAssembly y el soporte para el renderizado del robot 3D.

---

## 🏗️ 1. Estructura del Cliente (Blazor WebAssembly)

El frontend se ejecuta 100% en el navegador del cliente gracias a **Blazor WebAssembly (.NET 9)**, lo que proporciona una experiencia de aplicación de una sola página (SPA) rápida y fluida sin recargas completas.

### A. Organización de Vistas y Páginas (`Pages/`)
Las páginas se dividen de forma segura según el rol del usuario utilizando subcarpetas específicas:
*   **`Pages/Admin/`**: Contiene portales financieros (`Finanzas.razor`), vistas de clientes (`Cliente.razor`), paneles de control (`DashboardAdmin.razor`) y formularios.
*   **`Pages/Cliente/`**: Vistas exclusivas para el cliente (progreso del proyecto, pasarela de pago y agendamiento).
*   **`Pages/Empleado/`**: Vista del desarrollador/diseñador asignado para ver sus tareas.

### B. Hojas de Estilos Modularizadas (`wwwroot/css/`)
Para mantener el código ordenado y evitar un archivo `app.css` gigantesco e inmantenible, tu compañera modularizó los estilos de forma excelente por vistas:
*   `Calendario.css`: Controla los grid e interactividad del calendario de reuniones.
*   `Dashboard.css`: Estila las tarjetas de información, gráficos y barras de progreso.
*   `bitart-home.css`: Controla la estética de la Landing Page inicial.
*   `Otros.css` y `Registerrs.css`: Estilos para botones, modales y formularios de registro.

---

## 🤖 2. Carga y Visualización del Robot 3D (`.glb`)

La identidad visual única de BitArt incluye un robot interactivo en 3D en la página de inicio. Para lograr esto en .NET 9, implementamos dos optimizaciones clave:

### A. Reconocimiento de Archivos 3D en el Servidor (`Program.cs`)
Por defecto, los servidores IIS y Kestrel de ASP.NET Core no permiten la descarga de extensiones desconocidas como `.glb` o `.gltf` por razones de seguridad. Configuramos el backend para reconocer y permitir estos tipos MIME:

```csharp
var provider = new FileExtensionContentTypeProvider();
provider.Mappings[".glb"] = "model/gltf-binary";
provider.Mappings[".gltf"] = "model/gltf+json";

app.UseStaticFiles(new StaticFileOptions
{
    ContentTypeProvider = provider
});
```

### B. Visualizador 3D en Blazor (`ImageCarousel3D.razor`)
*   El modelo 3D oficial `robotbitart.glb` se encuentra guardado en `wwwroot/models/`.
*   Se renderiza interactivamente utilizando librerías del lado del cliente compatibles con WebGL.

---

## 🎨 3. Prácticas Clave para UI/UX Sostenible

Para que las futuras actualizaciones de tu socia no rompan la estética premium de la aplicación:
1.  **Consistencia de Colores**: Utilizar la paleta de colores HSL definida en las variables globales de CSS en `wwwroot/app.css` o `Dashboard.css`.
2.  **Micro-animaciones**: Todos los botones interactivos deben contar con transiciones suaves en CSS (`transition: all 0.3s ease`).
3.  **Responsividad**: Diseñar siempre pensando en dispositivos móviles primero utilizando Media Queries (`@media (max-width: 768px)`).
