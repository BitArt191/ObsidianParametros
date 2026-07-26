# Estudio de Precios y Modelo de Suscripciones (MRR)

Para que BitartCore sea rentable y no dependa de estar vendiendo proyectos nuevos todos los meses (el famoso ciclo de "fiesta o hambruna" de las agencias), debemos integrar el modelo **WaaS (Website as a Service) o SaaS B2B**.

Este modelo cambia el "te cobro una vez por hacerte la página" a "te cobro un costo inicial bajo de instalación (Setup) y una suscripción mensual por el servicio".

## 1. Análisis de los Precios Actuales en Colombia
*   **Landing Page Avanzada:** Setup de $800.000 COP
*   **Portal B2B / E-commerce:** Setup de $2.500.000 COP

Estos precios son **EXCELENTES como "Setup Fee" (Costo de Instalación)** para enganchar al cliente rápido, *siempre y cuando* vayan atados a una suscripción mensual obligatoria y se desarrollen clonando la plantilla base de BitartCore en .NET.

---

## 2. Márgenes de Ganancia de la Suscripción Mensual (El Secreto de la Rentabilidad)

Una preocupación muy válida es: *¿Acaso la mensualidad no se nos va a ir toda en dar soporte al cliente y pagar servidores?*

La respuesta es NO, si se estructura como un **SaaS automatizado**. Aquí está la matemática de por qué una suscripción de $250.000 COP (para el Plan 2) es altamente rentable:

### Costos Operativos vs Ganancia (Ejemplo Plan 2: $250.000 COP/mes)
*   **Costo de Servidor (Hosting/VPS):** Si usan un VPS (DigitalOcean/Contabo) de $20 USD mensuales, pueden alojar ahí hasta 15-20 portales. El costo real de servidor por cliente es de aprox. **$5.000 a $10.000 COP al mes**.
*   **Costo de Dominio y SSL:** ~$5.000 COP al mes.
*   **Costo de Soporte Técnico:** Aquí está el truco. "Soporte" **NO** significa "te voy a programar una vista nueva cada mes gratis". El soporte que incluye la suscripción es únicamente "Garantizar que el sistema esté encendido y sin errores". 
    * Como el cliente usa la plantilla BitartCore ultra-probada, los errores de código tienden a cero. El soporte será mínimo (ej. recuperar una contraseña, dudas de uso).
*   **Margen de Ganancia Limpio:** De los $250.000 COP, los gastos reales (sin contar la bolsa de horas de desarrollo adicional, que se cobra extra) son apenas de $15.000 COP. **El margen de ganancia es de casi un 90% (~$235.000 COP de utilidad pura por cliente cada mes).**

### Reglas de Oro para Proteger la Ganancia:
Para evitar que el cliente se consuma el tiempo de tu equipo (lo que llaman "Scope Creep"):
1. **Límites de Soporte Claros:** En el contrato debe decir: *"El soporte incluye resolución de caídas del servidor y bugs críticos. NO incluye desarrollos de nuevas funcionalidades ni rediseños"*.
2. **Cambios Menores Acotados:** (Especialmente en la Landing Page de $90.000/mes): "Incluye hasta 1 cambio de texto o imagen al mes. Cambios adicionales se cotizan por separado".
3. **Bolsa de Horas:** Si el cliente quiere un botón nuevo o un reporte nuevo en el CRM, eso se cobra aparte (Mantenimiento Evolutivo), o lo debe comprar en un plan "Retainer" mucho más caro (El Plan 3).

---

## 3. La Proyección de Rentabilidad (MRR)
*   Con **10 clientes** en el Plan 2: Tendrás **$2.500.000 COP fijos al mes**. El gasto en servidor para alojarlos a todos será de menos de $100.000 COP.
*   Con **40 clientes**: Tendrás **$10.000.000 COP fijos al mes**, lo que cubre el salario base del equipo fundador o desarrolladores, solo por mantener el software encendido.

Esto convierte a BitartCore en una empresa financiera y operativamente a prueba de balas.

---

## 4. Suscripciones para Desarrollo Personalizado (Retainers)

Para los proyectos a medida (Plan 3 - "SaaS, Apps & 3D"), la suscripción no es un simple hosting, sino un **Acuerdo de Nivel de Servicio (SLA) y Retainer**.

### Estrategia de Visibilidad de Precios
*Estratégicamente, **NUNCA** se debe poner el precio fijo de este Retainer en la página web pública.* 
El costo de servidores de un software a medida puede variar desde $50 USD hasta $500+ USD mensuales dependiendo de la arquitectura (bases de datos replicadas, uso de APIs de Inteligencia Artificial, balanceadores de carga). Mostrar un precio base puede "amarrarlos" a perder dinero. **Este precio se negocia siempre en la firma del contrato.**

### Rangos de Mercado en Colombia para Retainers de Software a Medida:
1.  **Retainer Básico (Mantenimiento y SLA): $800.000 a $1.500.000 COP / mes.**
    *   Incluye: Pago de infraestructura Cloud pesada (AWS/Azure), monitoreo de seguridad 24/7 y arreglo de bugs críticos urgentes. Cero desarrollo de código nuevo.
2.  **Retainer Evolutivo (Bolsa de Horas): $2.000.000 a $5.000.000+ COP / mes.**
    *   Incluye: Todo lo del básico + una bolsa de 10 a 20 horas mensuales de desarrollo de tu equipo. Ideal para clientes corporativos que siempre necesitan botones nuevos, reportes financieros o integraciones que evolucionan con su negocio mes a mes.
