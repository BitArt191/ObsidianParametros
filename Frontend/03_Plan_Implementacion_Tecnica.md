# Plan de Implementación Técnica: Landing Page Dinámica (Blazor + GSAP)

Este plan detalla los pasos técnicos para transformar el diseño actual de BitArt Core en una experiencia interactiva inmersiva, tomando como base las referencias de **andrewcunliffe.ai**, **Flowty**, y **Dreiraum Studio**.

---

## ⚠️ Decisiones Técnicas Críticas
1. **Reemplazo de librería de animación:** Actualmente el proyecto usa `AOS` (Animate on Scroll). Para lograr los efectos de "Scroll-jacking" (que el contenido reaccione a la posición de la rueda del ratón) y el modelo 3D dinámico, se **removerá `AOS`** y se utilizará **GSAP** (GreenSock) junto con su plugin `ScrollTrigger`.
2. **Reestructuración de Componentes:** El archivo `Home.razor` será modificado drásticamente a nivel de etiquetas HTML/CSS para soportar que el robot 3D flote a través de las secciones. El texto y el sentido de la página se mantendrán iguales, pero la estructura de contenedores cambiará.

---

## 🛠️ Cambios Propuestos en el Repositorio (`dev-frontend`)

A continuación se agrupan los archivos que serán modificados en el código fuente:

### Configuración Base y Librerías

*   **`App.razor` (Proyecto Server):**
    *   Se agregarán los scripts CDN de **GSAP** y **ScrollTrigger** en la sección `<head>` o antes del cierre del `<body>`.
    *   Se enlazará el nuevo archivo JavaScript para la interacción de JS a C#.

*   **`animations.js` (Nuevo Archivo en Cliente `wwwroot/JS/`):**
    *   Archivo que contendrá toda la lógica pura de GSAP:
        *   Función para rotar y mover el `<model-viewer>` según el scroll (Estilo Flowty).
        *   Función de Parallax para hacer flotar las tarjetas pequeñas (Floating UI).
        *   Función para el efecto de "explosión" o revelar tipografía (Estilo Andrew Cunliffe).

### Estilos (CSS) y Diseño Visual

*   **`app.css` (Cliente `wwwroot/css/`):**
    *   Efecto de **Ruido de Fondo (Grain)**.
    *   Clases para los **Bordes Iluminados** (gradientes morado/rosa estilo Dreiraum).
    *   Configuración del `z-index` para que el robot flote por encima/debajo de la tipografía gigante.
    *   Estilos para la **Barra de Navegación Flotante** (tipo píldora inferior).

### Componentes Blazor (Maquetación)

*   **`Home.razor` (Cliente `Pages/`):**
    *   **Rediseño Hero:** Tipografía gigante interactuando con el robot 3D.
    *   **Proyectos/Especialidades:** Cambiar el grid cuadrado estático por elementos "Floating UI" (tarjetas de cristal orbitando alrededor de un mockup central).
    *   **Precios (Planes):** Implementar tarjetas oscuras con gradientes iluminados y etiqueta destacada ("Popular").
    *   **Integración JS:** Se conectará JSInterop (`IJSRuntime`) para disparar las animaciones de GSAP en el método `OnAfterRenderAsync(bool firstRender)`.
