---
description: >-
  La API de envíos transaccionales te permite enviar los emails de tu aplicación
  a través de Perfit.
---

# Introducción

## Activa tu cuenta

Para empezar a utilizar el servicio de emails transaccionales, primero **debes generar tu API key**. Puedes hacerlo desde la sección **Integraciones** en tu cuenta de Perfit. 

Si tienes dudas sobre cómo hacerlo contáctanos a [soporte@myperfit.com](mailto:soporte@myperfit.com).

{% hint style="info" %}
El API key utilizada para los envíos transaccionales **es una API key específica**, distinta a la asociada a cada usuario \(la que se usa para gestión de contactos por ejemplo\)

Es fácil identificar sin un API key es para uso de envíos transaccionales, si contiene `tr` luego del nombre de cuenta:

`micuenta-tr-aDsffD35eSdfsadsGFdFfssfsaADS`
{% endhint %}

## Usos frecuentes

Algunos de los usos más frecuentes son:

* Emails de registración, bienvenida, …
* Emails de compra finalizada, carrito abandonado, …
* Notificaciones de cambio de plan, factura pendientes, pago realizado…
* Envío de notificaciones en general.

## Características principales

### Potente motor de reemplazo de contenido

Utiliza variables de reemplazo para enviar contenidos personalizados a cada destinatario. Contamos con uno de los motores más completos, que te permitirá entre otra cosas:

* **Bloques condicionales**. Por ejemplo, para mostrar ciertas partes del contenido dependiendo del perfil de cada destinatario.
* **Iteradores**. Muy útil para mostrar listados variables de productos.
* **Reemplazo de variables con valores por defecto.** Para dirigirte a cada destinatario en forma personal
* **Aplicar formatos a fechas, números, etc.** 

### Monitoreo de aperturas y clicks

Registramos en forma predeterminada las aperturas y clicks en todos los links del contenido.

### Gestión de desuscripciones

Opcionalmente puedes incluir un link en el contenido para que tus contactos se desuscriban.

### Versión online del contenido

También generamos una versión web del contenido. Así podrás incluir un link para ver el mensaje en el navegador.

### Notificaciones por webhooks

Recibe todos los eventos de envíos, aperturas, clicks y desuscripciones para sincronizar tus listas o actualizar el estado de tus contactos en la aplicación integrada.

### Envío programado

Es posible posponer el envío de los emails indicando una fecha futura. 

### Archivos adjuntos

Puedes incluir archivos adjuntos en tus envíos. Soportamos los formatos pdf, png, jpg, gif, txt, csv, xls, xlsx, doc, docx.

{% hint style="info" %}
Para habilitar el envío de archivos adjuntos, ponte en contacto con nosotros. Puedes solicitarlo a dev@myperfit.com.
{% endhint %}

