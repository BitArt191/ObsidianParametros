---
tags:
  - backend
  - conceptos
  - api
  - endpoints
---

# Conceptos Fundamentales: APIs, Endpoints y JSON

Para construir un puente sólido entre el Frontend y el Backend en BitArt Core, es vital dominar estos tres conceptos de la comunicación web corporativa.

## 1. ¿Qué es una API? (El Restaurante)
API significa *Interfaz de Programación de Aplicaciones*.
Imagínalo como un **Restaurante**:
- El **Frontend** es el *Cliente* que se sienta en la mesa y tiene hambre (quiere datos).
- El **Backend** es la *Cocina* donde están los ingredientes (Base de datos) y los chefs (lógica de negocio).
- La **API** es el *Mesero*. El cliente no puede entrar a la cocina a preparar su comida; tiene que hablar con el mesero, darle su orden (Petición) y esperar a que el mesero le traiga su plato listo (Respuesta).

## 2. ¿Qué es un Endpoint? (El Menú)
Si la API es el mesero, los **Endpoints** son los platos que están escritos en el *Menú*.
Un Endpoint es literalmente una dirección URL (una ruta) que el Backend expone para que el Frontend pueda consumir un servicio específico.

Un Endpoint se compone de dos partes fundamentales:
1. **El Verbo HTTP (La Acción):**
   - `GET`: "Tráeme información" (Ej: Obtener la lista de proyectos).
   - `POST`: "Toma esta información y crea algo nuevo" (Ej: Crear un nuevo administrador).
   - `PUT` / `PATCH`: "Actualiza algo que ya existe" (Ej: Cambiar la contraseña).
   - `DELETE`: "Borra algo" (Ej: Eliminar a un cliente).
2. **La Ruta (El Destino):**
   - `/api/Admin/create`
   - `/api/Clientes/listar`

Cuando Heidy desde el Frontend hace un `POST` a `https://api.bitart.com/api/Admin/create`, está pidiendo exactamente ese plato del menú.

## 3. ¿Qué es JSON? (El Idioma)
JSON (*JavaScript Object Notation*) es el idioma universal en el que el Frontend y el Backend se comunican. 
Como el Frontend está hecho en Blazor/WebAssembly y el Backend en C#, necesitan un idioma neutro para pasarse la información. JSON es simplemente texto estructurado que parece un diccionario.

**Ejemplo de Petición (Lo que envía el Frontend):**
```json
{
  "email": "nuevo@bitart.com",
  "password": "PasswordFuerte123!",
  "nombreCompleto": "Ana Torres"
}
```

**Ejemplo de Respuesta (Lo que devuelve el Backend):**
```json
{
  "message": "Administrador Ana Torres creado con éxito.",
  "status": 200
}
```

## Resumen en el Ecosistema BitArt
Tú (Backend) creas **Endpoints** en tus Controladores de C#. Heidy (Frontend) lee tu **Swagger** (el catálogo de tu Menú) para saber qué **JSON** enviarte. Cuando su código hace la petición al Endpoint correcto con el JSON correcto, ocurre la magia.
