---
description: >-
  La API SMTP permite enviar emails utilizando clientes SMTP sin necesidad de
  cambiar implementaciones existentes. La funcionalidad es algo más limitada que
  la API HTTP.
---

# Envío a través SMTP

## Host y puertos

La conexión debe hacerse a **`smtp.myperfit.com`**, a alguno de estos puertos: `25`, `587`, `2525`.

{% hint style="warning" %}
Algunos ISPs bloquean o limitan el tráfico del puerto 25, por lo que recomendamos utilizar el puerto 586.
{% endhint %}

## Autenticación

Debe utilizarse el método **`AUTH LOGIN`** para autenticarse con estas credenciales:

* username: **apikey**
* password: **&lt;&lt;MI\_API\_KEY&gt;&gt;**

{% hint style="info" %}
Por el momento sólo es posible generar los API keys enviando una solicitud a [dev@myperfit.com.](mailto:dev@myperfit.com)
{% endhint %}

## Limitaciones

La API SMTP por el momento cuenta con estas limitaciones:

* No es posible modificar las opciones de monitoreo. Por defecto está activado el monitoreo de aperturas y clicks.
* No es posible indicar modelos para utilizar en el motor de reemplazo \(`substitutions`\)
* No es posible indicar `tags`, `custom_args`, `batch_code`.
* Por el momento no es posible enviar archivos adjuntos \(la API HTTP tampoco lo permite\).

Si necesitas utilizar algunas de estas características utiliza la API HTTP.

## Ejemplo utilizando telnet

Las líneas maracadas con &gt; son las que deben escribir.

```text
> telnet smtp.myperfit.com 587
Trying 34.238.225.76...
Connected to smtp-transactional-prod-173515567.us-east-1.elb.amazonaws.com.
Escape character is '^]'.
220 localhost ESMTP Perfit v2

> EHLO minombre
250-smtp.myperfit.com
250-8BITMIME
250-SIZE 10000
250-AUTH LOGIN
250 Ok

> AUTH LOGIN
334 VXNlcm5hbWU6

> YXBpa2V5
334 UGFzc3dvcmQ6

> <<API KEY en base64>>
235 Authentication successful.

> MAIL FROM: yo@midominio.com
250 Ok

> RCPT TO: destinatario@domain.com
250 Ok

> DATA
354 End data with <CR><LF>.<CR><LF>
Subject: este es el asunto

Este es el contenido
.
250 Ok
```



