---
description: >-
  La API SMTP permite enviar emails utilizando clientes SMTP sin necesidad de
  cambiar implementaciones existentes. La funcionalidad es algo más limitada que
  la API HTTP.
---

# Envío a través SMTP

## Host y puertos

La conexión debe hacerse a **`smtp.myperfit.com`** utilizando el puerto: **`2525`**.

## Cifrado

En esta opción selecciona la opción **Ninguno** o **Sin cifrado**.

{% hint style="info" %}
Por el momento no soportamos opciones de cifrado como SSL o TLS.
{% endhint %}

## Autenticación

Debe utilizarse el método **`AUTH LOGIN`** para autenticarse con estas credenciales:

* username: "**apikey"**
* password: **MI\_API\_KEY**

**Por ejemplo:**

* username: **apikey**
* password: **micuenta-tr-lf223iewndfc09wopijqesdqws**

{% hint style="success" %}
Puedes **generar tu API key** desde la sección **Integraciones** en tu cuenta de Perfit. 

Si tienes dudas sobre cómo hacerlo contáctanos a [soporte@myperfit.com](mailto:soporte@myperfit.com).
{% endhint %}

## Limitaciones

La API SMTP por el momento cuenta con estas limitaciones:

* No es posible modificar las opciones de monitoreo. Por defecto está activado el monitoreo de aperturas y clicks.
* No es posible indicar modelos para utilizar en el motor de reemplazo \(`substitutions`\)
* No es posible indicar `tags`, `custom_args`, `batch_code` para identificar eventos o agrupar envíos.

Si necesitas utilizar algunas de estas características por favor utiliza la API HTTP.

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



