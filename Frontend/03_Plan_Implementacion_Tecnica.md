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

1. **Scroll-Jacking del Robot:**
   - Hacer que el robot 3D baje a través de las secciones, reaccionando a la posición de la rueda del ratón (Estilo Flowty).
2. **Revelado de Tipografía:**
   - Animación en cascada para el título principal del Hero.
3. **Floating UI (Parallax):**
   - Hacer que las tarjetas floten levemente en dirección contraria al movimiento del ratón.
4. **Iluminación Dinámica del Modelo 3D:**
   - Ajustar la exposición y las sombras del `model-viewer` mediante código para que se mezcle con los fondos morados/oscuros.
