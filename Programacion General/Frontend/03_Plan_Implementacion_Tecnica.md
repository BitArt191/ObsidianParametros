# Plan de Implementación: Landing Page (Paso a Paso)

Este documento centraliza la hoja de ruta para llevar la Landing Page de BitArt Core al nivel "Awwwards", priorizando primero el diseño visual estático y luego las animaciones complejas.

## Fase 1: Maquetado "Dark Premium" (Actual)
El objetivo es lograr la estética visual de nuestras referencias (fondos oscuros, textos claros, bordes iluminados) sin interferencia de animaciones.

1. **Inversión de Paleta (Dark Mode):**
   - Cambiar todos los fondos blancos (`#ffffff`) a oscuros (`#0a0b10`).
   - Invertir textos oscuros a blancos/grises claros.
2. **Rediseño del Header (Navegación):**
   - Implementar "Glassmorphism" (fondo oscuro semi-transparente con desenfoque) en lugar del fondo blanco sólido.
3. **Estructura de Tarjetas (Bento Box):**
   - Aplicar diseño oscuro con la clase `.ba-glow-border` (estilo Dreiraum) a:
     - Especialidades.
     - Metodología.
     - Planes y Precios.
4. **Pausar Animaciones Complejas:**
   - Desactivar temporalmente el recorrido del Robot 3D por la página para evitar que rompa el layout visual mientras se maqueta.

---

## Fase 2: Animaciones e Interacción (GSAP)
Una vez que el maquetado estático sea 100% perfecto, reactivaremos y puliremos las animaciones.

### 1. Scroll-Jacking del Robot (Completado/En Pruebas)
Se implementó un sistema de Scroll-Jacking estilo Flowty.co para que el modelo 3D viaje por la página.
**Detalles de Implementación:**
- **Contenedor Global:** El `<model-viewer>` se extrajo del Hero y se colocó en `<div id="global-3d-container">` con `position: fixed` y `pointer-events: none` para flotar sobre todo sin bloquear clics.
- **Control de GSAP:** En `animations.js` se creó un timeline global (`scrub: 1`) que mueve el modelo mediante transformaciones (x, y, scale, rotationZ) a medida que el usuario baja por `#inicio`, `#nosotros`, `#servicios`, `#proyectos` y `#contacto`.
- **Interacción Manual Desactivada:** Para evitar conflictos y problemas de UX, la rotación manual (arrastrar con el mouse) fue deshabilitada; el robot rota automáticamente (`auto-rotate`).
- **Adaptabilidad (Móviles):** Mediante `ScrollTrigger.matchMedia()`, en pantallas menores a 992px el modelo permanece quieto en el Hero y luego se desvanece suavemente para mejorar el rendimiento.

### 2. Revelado de Tipografía
- Animación en cascada para el título principal del Hero.

### 3. Floating UI (Parallax)
- Hacer que las tarjetas floten levemente en dirección contraria al movimiento del ratón.

### 4. Iluminación Dinámica del Modelo 3D
- Ajustar la exposición y las sombras del `model-viewer` mediante código para que se mezcle con los fondos morados/oscuros.
