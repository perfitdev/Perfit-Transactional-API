# Autenticación, formatos y límites

## Autenticación

La autenticación se realiza mediante el header `Authorization: Bearer <<API_KEY>>`.

{% hint style="danger" %}
**NUNCA se debe incluir el API key en código del lado cliente, por ejemplo javascript del navegador. Utilizar SIEMPRE del lado servidor.**
{% endhint %}

{% hint style="info" %}
Por el momento sólo es posible generar los API keys enviando una solicitud a [dev@myperfit.com.](mailto:dev@myperfit.com)
{% endhint %}

## Formatos

### Fechas

Todas las fechas deben indicarse en formato **ISO-8601**, por ejemplo: `2018-11-06T23:12:00Z` o`2018-11-06T23:12:00-03:00`

Los eventos se indican siempre usando el huso horario **UTC**.

### Content-Type

Se acepta únicamente contenidos de tipo `application/json`, debiendo siempre indicarse en el header `Content-Type`.

### Encoding y Charset

El encoding soportado para los requests es **UTF-8**. Todos los strings deben utilizar el charset **Unicode**.

### Direcciones de email

Todas las direcciones de email deben válidas, tal como se especifica en [RFC-5322](https://tools.ietf.org/html/rfc5322#section-3.4.1).

## Límites

### Límite de destinatarios

La cantidad máxima de `recipients` por request es de 1000.

### Limite total por request

El tamaño total de cada request no puede superar los 10MB.

### Limite de contenidos

Cada contenido \(`html` o `text`\) no pueden superar los 300KB.

### Limite de CCs y BCCs

La cantidad máxima direcciones CC y BCC es de 10 para cada recipient.

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

## Códigos de error

| Error | Descripción |
| :--- | :--- |
| `required` | El campo es requerido. |
| `required_at_least_one` | Se debe incluir al menos un elemento en el campo de tipo array. |
| `max_length_exceeded` | Se excedió la longitud máximo en un campo de tipo string. |
| `too_many_items` | Se excedió la cantidad permitida de elementos en un campo de tipo array. |
| `invalid_value` | El valor indicado no es válido. |



