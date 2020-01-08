# Autenticación y formatos

## Autenticación

La autenticación se realiza agregando el header `Authorization` a cada request: 

```text
Authorization: Bearer MI_API_KEY
```

#### Por ejemplo:

```text
Authorization: Bearer aDsffD35eSdfsadsGFdFfssfsaADS
```

{% hint style="danger" %}
**NUNCA se debe incluir el API key en código del lado cliente, como por ejemplo javascript del navegador. Utilizarlo SIEMPRE del lado servidor \(php, java, node, …\)**
{% endhint %}

{% hint style="info" %}
Puedes generar tu API keys desde la sección Integraciones de tu cuenta de Perfit. Si tienes dudas sobre cómo hacerlo contáctanos a [soporte@myperfit.com](mailto:soporte@myperfit.com).
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



