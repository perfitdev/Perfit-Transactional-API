# Formatos

## Fechas

Todas las fechas deben indicarse en formato **ISO-8601**, por ejemplo: `2018-11-06T23:12:00Z` o`2018-11-06T23:12:00-03:00`

Los eventos se indican siempre usando el huso horario **UTC**.

## Content-Type

Se acepta únicamente contenidos de tipo `application/json`, debiendo siempre indicarse en el header `Content-Type`.

## Encoding y Charset

El encoding soportado para los requests es **UTF-8**. Todos los strings deben utilizar el charset **Unicode**.

## Direcciones de email

Todas las direcciones de email deben válidas, tal como se especifica en [RFC-5322](https://tools.ietf.org/html/rfc5322#section-3.4.1).

