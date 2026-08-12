---
tags:
  - backend
  - arquitectura
  - entrevista
  - patrones
---

# Guía de Entrevistas: Arquitectura de BitArt Core

Este documento traduce la teoría aburrida de las entrevistas técnicas a la **práctica real** de lo que hemos construido en BitArt Core. ¡Si te preguntan en una entrevista, responde usando tu propio proyecto!

## 1. ¿Qué Arquitectura estamos usando en BitArt Core?

Si un reclutador te pregunta: *"¿Qué arquitectura usas en tus proyectos .NET?"*
**Tu respuesta Senior:** *"Actualmente en BitArt Core implementé una **Arquitectura Monolítica en Capas (N-Tier)** con fuertes inspiraciones en **Clean Architecture**."*

**¿Por qué respondes eso? (La justificación real):**
- **Es un Monolito:** Toda la API, la conexión a la base de datos y la lógica viven en un solo servidor de despliegue (`APPWebBitArt`). Esto es la mejor práctica para un MVP de Startup porque reduce los costos de infraestructura y acelera el desarrollo.
- **En Capas (N-Tier):** Tenemos separación horizontal:
  - Capa de Presentación/API: Nuestros `Controllers` (ej. `ClientesController`).
  - Capa de Datos: Nuestro `ApplicationDbContext` y Entity Framework.
- **Inspiración Clean Architecture:** Tenemos un proyecto separado llamado `BitArt.Shared` donde viven nuestras Entidades (el núcleo de negocio). El proyecto principal depende de Shared, y no al revés.

## 2. ¿Por qué no usamos Microservicios?

Si el reclutador te presiona: *"¿Y por qué no usaste Microservicios si es lo más moderno?"*
**Tu respuesta Senior:** *"La arquitectura debe resolver problemas de negocio, no seguir modas. Los microservicios resuelven problemas de escalabilidad extrema y equipos de cientos de desarrolladores (como Mercado Libre o Netflix). Para una Startup en fase de MVP, un microservicio introduce complejidad innecesaria (latencia de red, despliegues complejos, eventual consistency). Empezamos con un Monolito bien estructurado; si en el futuro BitArt crece a millones de usuarios, tenemos el código tan limpio (con interfaces) que transicionar a un **Monolito Modular** o Microservicios será un proceso natural, no una reescritura traumática."*

## 3. ¿Qué Patrones de Diseño usamos?

En BitArt Core aplicamos patrones todos los días sin darnos cuenta:

1. **Patrón Repositorio (Structural/Architectural):**
   - *Dónde:* `IRepository<T>`, `ClienteRepository`.
   - *Por qué:* Aísla la lógica de acceso a datos (Entity Framework) de la lógica de negocio (Controladores).
2. **Inyección de Dependencias (DI) / IoC:**
   - *Dónde:* En `Program.cs` cuando hacemos `builder.Services.AddScoped<IClienteRepository, ClienteRepository>()`.
   - *Por qué:* Desacopla la creación de objetos. El controlador pide un `IClienteRepository` y el sistema (una especie de patrón **Factory** interno de .NET) le inyecta la instancia correcta.
3. **Singleton (Lifetime):**
   - *Dónde:* Aunque usamos `AddScoped` para repositorios (viven por petición), componentes internos de .NET como la caché o la configuración (`appsettings.json`) se inyectan como **Singleton** (una sola instancia para toda la app).
4. **Decorator / Middleware (Estructural):**
   - *Dónde:* La etiqueta `[Authorize]` funciona conceptualmente como un Decorator. Añade comportamiento de seguridad antes de ejecutar el controlador, sin modificar el código interno del controlador.
