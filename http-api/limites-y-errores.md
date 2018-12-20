# Límites y errores

## Límites

### Longitudes máximas

| Campo | Longitud máxima por elemento | Cantidad máxima |
| :--- | :--- | :--- |
| `subject` | 200 chars | - |
| `recipients[]` | - | 1000 |
| `cc[]` | - | 10 |
| `bcc[]` | - | 10 |
| `name` \(from, to, cc, bcc\) | 100 chars | - |
| `headers[]` | - | 10 |
| `headers[].key` | 900 chars | - |
| `headers[].value` | 50 chars | - |
| `tags[]` | 100 chars | 10 |
| `batch_code` | 30 chars | - |
| html | 300KB |  |
| text | 300KB |  |

### Tamaño total por request

El tamaño total de cada request no puede superar los 10MB.

## Errores

Si ocurrió algo que impidió completar con éxito un pedido, la respuesta tiene esta forma: 

```javascript
{
    "success": false,
    "error": {
        "status": 403,
        "type": "forbidden",
        "message": "Origin IP address not allowed: 190.19.245.237"
    }
}
```

### Tipos de errores

El `type` puede ser alguno de estos:

| Status | error.type | Descripción |
| :--- | :--- | :--- |
| 400 | `bad_request` | El contenido del request tiene un formato inválido. |
| 400 | `validation_error` | Algunos de los campos tienen contenido inválido. |
| 401 | `unauthorized` | El API key utilizado es inválido o no se especificó. |
| 403 | `forbidden` | El request fue bloqueado. La causa se especifica en message. |
| 500 | `internal_server_error` | Ocurrió un error inesperado en el servidor. |
| 503 | `service_unavailable` | El servicio no está disponible. Generalmente por límites temporales de envío. |

### Errores de validación

Cuando `type` es `validation_error`, se incluye un objeto `errors` con todos los errores de validación encontrados:

```javascript
{
    "success": false,
    "error": {
        "status": 400,
        "type": "validation_error",
        "message": "Some fields have invalid values"
        "errors": {
            "from.email": "required"
        }
    }
}
```

Los tipos de error de validación pueden ser:

| Error | Descripción |
| :--- | :--- |
| `required` | El campo es requerido. |
| `required_at_least_one` | Se debe incluir al menos un elemento en el campo de tipo array. |
| `max_length_exceeded` | Se excedió la longitud máximo en un campo de tipo string. |
| `too_many_items` | Se excedió la cantidad permitida de elementos en un campo de tipo array. |
| `invalid_value` | El valor indicado tiene un formato inválido. |



