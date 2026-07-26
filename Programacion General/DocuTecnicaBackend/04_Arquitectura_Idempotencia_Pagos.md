---
tags:
  - backend
  - arquitectura
  - pagos
  - idempotencia
---

# Idempotencia en Pagos (Sprint 4)

## 🧠 Concepto Crítico para Milena: Idempotencia

La **idempotencia** es una propiedad matemática aplicada a la ingeniería de software que garantiza que:
> **"Una misma petición debe producir el mismo resultado, aunque se envíe varias veces."**

En el contexto de APIs REST, si un cliente hace una petición HTTP repetidas veces por error (ej. doble clic) o por problemas de red (ej. timeouts y reintentos automáticos del cliente), el sistema backend debe ser capaz de identificar que se trata de la misma intención y no duplicar el efecto secundario.

### ❌ El Problema (Sin Idempotencia)
1. El usuario hace clic en "Pagar".
2. El frontend envía un `POST /api/payments`.
3. El backend cobra la tarjeta y guarda el pago en SQL Server.
4. Por latencia, el frontend cree que falló y **reintenta** el `POST /api/payments`.
5. El backend vuelve a cobrar la tarjeta y guarda un SEGUNDO pago.
**Resultado:** Cliente enfurecido por doble cobro.

### ✔️ La Solución (Con Idempotencia)
1. El usuario hace clic en "Pagar".
2. El frontend genera un UUID único y envía: `POST /api/payments` con el header `Idempotency-Key: abc-123`.
3. El backend verifica si ya procesó la clave `abc-123`. Como no la tiene, cobra la tarjeta, guarda el pago y registra la clave como "completada".
4. El frontend reintenta: `POST /api/payments` con el mismo header `Idempotency-Key: abc-123`.
5. El backend ve que la clave `abc-123` ya existe y fue completada. **No vuelve a cobrar**. Simplemente devuelve la misma respuesta exitosa que la primera vez.

---

## 🏗️ Implementación Requerida para BitArt Core (Sprint 4)

Dado que en nuestro **Sprint 4** construiremos la pasarela de pagos y utilizaremos la tabla `Payments`, implementaremos este mecanismo en nuestros controladores.

**Checklist Técnico para Sprint 4:**
- [ ] Crear un Middleware o ActionFilter en ASP.NET Core que intercepte el header `Idempotency-Key`.
- [ ] Configurar un sistema de almacenamiento rápido (ej. una pequeña tabla en SQL Server o Redis) para recordar qué *Idempotency Keys* ya fueron procesadas durante las últimas 24 horas.
- [ ] Asegurarnos de que Heidy en el frontend genere y envíe un UUID único por cada intento legítimo de transacción.
