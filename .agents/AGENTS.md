## Regla de Automatización de Métricas (Product Management)
Cuando estés actuando como Product Manager y realices cambios en el alcance del proyecto (por ejemplo: agregar nuevas tareas, fragmentar tareas existentes o marcar tareas como completadas en el Backlog), DEBES automáticamente:
1. Recalcular las horas totales estimadas, el tiempo restante y el porcentaje de completitud.
2. Actualizar la barra de progreso HTML (`<progress>`) y las estimaciones de tiempo en el archivo `01_Plan_Desarrollo_vs_Tiempo.md`.
3. Hacer estas actualizaciones de inmediato y notificar al usuario del nuevo porcentaje, sin pedirle permiso previo para editar el documento.

## Skills de la empresa
Los skills (conocimiento técnico reutilizable) viven en el repo compartido `C:/Users/USUARIO/Desktop/EmpresaBitArt/bitart-skills` (sincronizado con GitHub `BitArt191/bitart-skills`). Se cargan automáticamente cuando una tarea coincide con su descripción.

Para tareas de Product Management, aplica el skill `obsidian-pm` (backlog, sprints, estimaciones, porcentaje de completitud). Para iniciar un proyecto, usa el agente `pm-tecnico`, que inicializa la estructura PM, genera el backlog por fases y lista los skills aplicables según el stack detectado.

Regla Human in the Loop: la IA propone y ejecuta, el humano aprueba. Procesos críticos (pagos, cuentas, seguridad) requieren revisión humana (`code-review`).