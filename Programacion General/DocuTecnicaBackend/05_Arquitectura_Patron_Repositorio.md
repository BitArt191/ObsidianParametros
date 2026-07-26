---
tags:
  - backend
  - arquitectura
  - patrones-diseno
---

# Patrón Repositorio en C#

## 🧠 Concepto Crítico para Milena: ¿Qué es y por qué usarlo?

El **Patrón Repositorio** es una de las prácticas más comunes e importantes en la arquitectura de software de nivel corporativo (Clean Architecture). Actúa como un intermediario o "mesero" entre la lógica de negocio (nuestros Controladores) y el acceso a datos (nuestro `ApplicationDbContext` de Entity Framework).

### ❌ El Problema (Sin Repositorio)
Si un controlador guarda un registro llamando directamente a `_context.Clientes.Add()`, nuestro controlador queda fuertemente acoplado a Entity Framework Core y a SQL Server. 
Si el día de mañana la empresa decide cambiar a una base de datos NoSQL (como MongoDB) o cambiar el ORM (por Dapper), tendríamos que reescribir docenas o cientos de controladores. Además, se vuelve muy difícil hacer pruebas unitarias (Unit Tests).

### ✔️ La Solución (Con Repositorio)
El controlador simplemente le pide a una interfaz (`IRepository`): *"Por favor, guarda este Cliente"*.
Al controlador **no le importa** cómo se guarda, ni dónde. Toda esa lógica sucia de SQL se esconde dentro de una clase específica que implementa el repositorio.

## 🏗️ Nuestro Enfoque Híbrido
Para `BitArt Core`, construiremos una solución profesional escalable:
1. **Repositorio Genérico (`IRepository<T>`)**: Una interfaz base con métodos que aplican para cualquier tabla (Crear, Leer por ID, Leer Todos, Actualizar, Borrar).
2. **Repositorios Específicos (`IAdminRepository`)**: Interfaces que heredan del genérico, pero añaden funciones exclusivas de esa entidad (Ej: `ObtenerAdminPorDniAsync()`), manteniendo el código limpio y respetando el principio SOLID de Responsabilidad Única.
