---
description: >-
  Desafortunadamente, no siempre sale todo bien! Es importante detectar y
  manejar todos los errores en forma adecuada.
---

# Manejo de errores

## Status codes

En caso de que ocurra un error, el status recibido será uno de los siguientes:

| **Code** | **Status** | **Significado** |
| :--- | :--- | :--- |
| `400` | `Bad Request` | Petición inválida |
| `401` | `Unauthorized` | Las credenciales de acceso no son válidas |
| `403` | `Forbidden` | El recurso solicitado no esta dentro de los permitidos |
| `404` | `Not found` | La URI solicitada no corresponde a ningun recurso |
| `405` | `Method Not Allowed` | El método HTTP no está soportado |
| `409` | `Conflict` | El recurso que se intenta crear o modificar entra en conflicto con uno existente |
| `415` | `Unsupported Media Type` | El Content-Type del pedido no es soportado |
| `500` | `Internal Server Error` | Error del servidor |
| `503` | `Service Unavailable` | El servidor está limitando el acceso al recurso |

## Detalles del error

Como complemento, la respuesta contendrá un objeto `error` con una propiedad `status` coincidente con la del status HTTP y un `type` que indica el motivos específico del error. 

Por ejemplo:

```javascript
{
    "href": "/micuenta/contacts",
    "success": false,
    "error": {
        "status": 409,
        "type": "RESOURCE_EXISTS",
        "userMessage": "El pedido no puedo ser procesado ya que entra en conflicto con un recurso existente",
        "validationErrors": {
            "email": "Valor duplicado"
        }
    }
}
```

Los valores de `type` pueden ser los siguientes:

| **Type** | **Descripción** |
| :--- | :--- |
| `BAD_REQUEST` | El pedido tiene una estructura inválida. |
| `RESOURCE_EXISTS` | El recurso que se intentó crear entra en conflicto con uno existente. Se indica en `validationErrors` los campos en conflicto. |
| `UNSUPPORTED_MEDIA_TYPE` | El formato de datos indicado no es soportado. |
| `INTERNAL_ERROR` | Ocurrió un error interno del servidor. |
| `METHOD_NOT_ALLOWED` | El método HTTP utilizado no es soportado por el recurso especificado. |
| `NOT_FOUND` | El recurso especificado no existe, puede ser porque el ID especificado no exista. |
| `SERVICE_UNAVAILABLE` | El recurso solicitado no esta disponible temporalmente, posiblemente debido a un exceso de carga. |
| `UNAUTHORIZED` | No se proporcionó `token` de autorización, o es inválido. |
| `FORBIDDEN` | No se dispone del permiso necesario para el recurso solicitado. |
| `VALIDATION_ERROR` | El pedido realizado contiene errores en uno o más campos, en `validationErrors` se indican los campos con errores. |
| `ACCOUNT_REQUIRED` | Se intentó realizar un login utilizando un email registrado en más de una cuenta, se debe repetir especificando la cuenta. En `data` se indican las cuentas posibles. |
| `PASSWORD_EXPIRED` | Se intentó realizar un login pero la contraseña esta expirada o debe ser renovada. |

