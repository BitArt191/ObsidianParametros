---
tags:
  - pm
  - riesgos
  - incertidumbre
---

# 02_Analisis_Riesgos_Incertidumbre

## ⚠️ Análisis de Riesgos e Incertidumbre

Como tu Product Manager, mi trabajo no solo es planificar el "camino feliz", sino prever dónde podemos tropezar. Aquí está nuestro análisis para el desarrollo en .NET profesional.

### 🌪️ Cono de Incertidumbre

Al inicio del proyecto, las estimaciones pueden desviarse significativamente. Dado tu objetivo de convertirte en una desarrolladora **Senior .NET**, la incertidumbre técnica es controlable porque estamos aplicando Arquitectura Limpia y patrones sólidos. El riesgo principal radica en la constancia y en dominar las integraciones complejas (Identity, JWT, Blazor WASM).

### 🛡️ Matriz de Riesgos

| ID | Riesgo | Probabilidad | Impacto | Estrategia de Mitigación (Plan de Acción) |
|----|--------|--------------|---------|-------------------------------------------|
| R-01 | **Falta de Continuidad Temporal** *(perder el hilo por pausas de días)* | Alta | Alto | Documentar exhaustivamente en código y usar el `03_Backlog_Tareas.md`. Al terminar el día, dejar un TODO explícito de por dónde empezar la siguiente sesión. |
| R-02 | **Bugs específicos de Integración** *(Identity, JWT con Blazor)* | Media | Alto | Dado que .NET unifica, pero separa API de WASM, es vital compilar y probar regularmente (con `xUnit`). No esperar a terminar todo para probar el login. |
| R-03 | **Feature Creep** *(Añadir ideas geniales sobre la marcha)* | Alta | Medio | Ser despiadados con el alcance. Si surge una nueva idea, se anota al final del Backlog. No interrumpe el sprint actual. |
| R-04 | **Desincronización del Equipo (Cuellos de Botella)** *(El Frontend avanza más rápido que el Backend o viceversa)* | Alta | Alto | Dado que tienen horarios distintos (10h vs 12h), usaremos **contratos de API (Swagger/Interfaces)**. Tú defines cómo responderá el backend, y tu socia puede avanzar con datos falsos (mockups) sin esperarte. |
| R-05 | **Curva de Aprendizaje (Overhead de tiempo)** *(Aprender a nivel Senior ralentiza la entrega inmediata)* | Media | Medio | Es un riesgo planeado. Aceptamos que una tarea tome 1 hora extra si eso implica que entiendas *por qué* usamos un patrón de diseño. El chat de código priorizará explicarte la arquitectura antes de darte el código copypaste. |
| R-06 | **Complejidad de Despliegue en la Nube** *(Azure/CI-CD)* | Baja | Alto | Invertir tiempo sólido en definir el esquema de datos y de CI/CD correcto antes de lanzar la Versión 1.0 a producción. |

### 📈 Plan de Revisión

Revisaremos este documento cada 3 semanas (aproximadamente 18 horas de desarrollo) para reevaluar si nuevos riesgos técnicos han surgido.
