---
description: >-
  Puedes configurar webhooks HTTP para recibir notificaciones ante ciertos
  eventos, como las aperturas, clicks, desuscripciones y rebotes.
---

# Webhooks de eventos

## Configuración

Por el momento no está disponible la API de administración de webhooks. Sólo es posible configurarlos  a pedido. 

{% hint style="info" %}
Puedes solicitar la configuración de un webhook enviando un email a [dev@myperfit.com](mailto:dev@myperfit.com).
{% endhint %}

Para cada webhook se debe indicar:

* URL de notificacion
* Eventos a notificar

## Tipos de eventos

### **Eventos de entrega**

* `track.mail.dropped`: El email fue descartado antes de intentar enviarlo. Puede deberse a un rebote o desuscripción previa.
* `track.mail.sent`: El email fue enviado. Esto no implica que haya sido entragado con éxito.
* `track.mail.bounced`: El email rebotó. Puede ser un rebote temporal \(SOFT\) o definitivo \(HARD\).

### **Eventos de actividad**

* `track.mail.opened`: Se detectó una apertura.
* `track.mail.first_opened`: Primera apertura sobre un envío \(evento único por cada `mail_id`\).
* `track.mail.clicked`: Se detectó un click sobre un link monitoreado.
* `track.mail.first_clicked`: Primer click sobre un envío \(evento único por cada `mail_id`\).
* `track.mail.unsubscribed`: El contacto se desuscribió o marcó el correo como spam.
* `track.mail.viewed_online`: Se producjo una visualización online.
* `track.mail.shared`: Se compartió el contenido utilizando el link de compartir en redes sociales.

## Notificaciones <a id="notificacion"></a>

Al generarse un evento para el cual existe un webhook configurado, se realizará un POST a la URL indicada. Se incluirá en el body del request un array con un conjunto de objetos, cada uno correspondiente a un evento único.

El procesamiento de los eventos deberá soportar recibir uno o varios eventos en un mismo POST. Los eventos agrupados pueden ser de distintos tipos. 

Por ejemplo:

```javascript
[
    {
        "timestamp": "2018-11-08T10:10:00Z",
        "track_id": "event_cjo4rwa3l0hqt0747awzl9jw2",
        "track_type": "track.mail.opened" , 
        ...
    },
    {
        "timestamp": "2018-11-08T10:10:02Z",
        "track_id": "event_cjoiasdf8uoieadscoiljadso",
        "track_type": "track.mail.clicked" , 
        ...
    },
    ...
]
```

### Respuesta y reintentos

Si el POST realizado recibe un código de respuesta distinto a 2xx, los eventos serás reencolados para su reintento. Se reintentará una vez más después de 1 minuto, luego los eventos serás descartados.

{% hint style="warning" %}
Si el volúmen de emails enviados genera muchos eventos, los webhooks pueden rápidamente sobrecargar al sevidor destino si no está configurado correctemente. Recomendamos utilizar loader.io para realizar pruebas de carga.
{% endhint %}

### Throttling

Para evitar sobrecargar al lado receptor, se limita la cantidad de requests por segundo a una misma URL a 250 requests/segundo.

## Detalles de los eventos

Todos los eventos incluyen cierta información básica. Además, dependiendo el tipo de evento, también se incluyen otros datos particulares.

### Información General

La información presente en todos los eventos es:

* `timestamp`: Fecha y hora de generación del evento.
* `sent_timestamp`: Fecha y hora de envío del email asociado al evento
* `hour_of_day`: Hora del día del `timestamp` \(0-23\).
* `day_of_week`: Día de la semana del `timestamp` \(1-7\).
* `track_id`: Id único del evento.
* `track_type`: Tipo de evento
* `batch_id`: Id asociado al batch. Si se indicó batch\_code en el request original tendra la forma: "nombrecuenta\_transactional\_batchcode"
* `mail_id`: Id asociado al email enviado.
* `mail_type`: Tipo de email, en este caso será siempre "transactional".
* `account`: Nombre de la cuenta.
* `email`: Dirección de email indicada en `recipient.to`
* `domain`: Dominio del email.
* `tags`: Array de etiquetas asociadas al batch, indicadas en el request de envío.
* `custom_args`: Objeto asociado al recipient, indicado en el request de envío.
* `mta`: Host utilizado para el envío del email.

### Eventos `track.mail.opened` y `track.mail.first_opened` <a id="evento-track-mail-opened"></a>

Además de la información básica, se incluyen también: 

* `user_agent`: string original del header User-Agent.
* `os_class`: Tipo de dispositivo: Mobile, Desktop, etc.
* `os`: Sistema operativo
* `os_version`: Sistema operativo y versión.
* `agent_name`: Nombre de cliente de correo
* `agent_version`:Nombre y versión de cliente de correo.
* `ip`: Dirección IP del cliente.
* `country`: País detectado a partir de la IP.
* `city`: Ciudad detectada a partir de la IP.
* `seconds_from_sent`: segundos transcurridos desde el evento track.mail.sent asociado a este evento. Sólo disponible en `track.mail.first_opened`.

Para los casos en que el pixel de trackeo de apertura se abra a través de un proxy \(por ejemplo Gmail y Yahoo\), no se incluye la información de geolocalización e identificación de dispositivo ya que no son confiables.

#### Ejemplo

```javascript
{
    "timestamp": "2018-11-05T20:43:34Z",
    "hour_of_day": 20,
    "day_of_week": 1
    
    "track_id": "event_cjo4rwa3l0hqt0747awzl9jw2",
    "track_type": "track.mail.opened",
​
    "batch_id": "micuenta_transactional_mibatchcode",
    "mail_id": "mail_cjo4qnh1242rl0833208jhofl",
    "mail_type": "transactional",
    "account": "micuenta",
    "email": "john@example.com",
    "domain": "example.com",
    
    "tags": [],
    "custom_args": {},
    
    "ip": "64.76.21.178",
    "country": "AR",
​
    "user_agent": "Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36",
    "os_class": "Desktop",
    "os": "Windows NT",
    "os_version": "Windows 7",
    "agent_name_version": "Chrome 70",
    "agent_name": "Chrome"
}
```

### Evento `track.mail.clicked` y `track.mail.first_clicked` <a id="evento-track-mail-clicked"></a>

Además de toda la información disponible en `track.mail.opened`, se incluye también:

* `url`: URL del link.
* `link_id`: Id único asociado al link.
* `interests`: Array de intereses si fueron indicados en el link.

#### Ejemplo

```javascript
{
    "timestamp": "2018-11-05T20:43:34Z",
    "hour_of_day": 20,
    "day_of_week": 1
    
    "track_id": "event_cjo4rwa3l0hqt0747awzl9jw2",
    "track_type": "track.mail.opened",
​
    "batch_id": "micuenta_transactional_mibatchcode",
    "mail_id": "mail_cjo4qnh1242rl0833208jhofl",
    "mail_type": "transactional",
    "account": "micuenta",
    "email": "john@example.com",
    "domain": "example.com",
    "contact_id": "276889",
    
    "tags": [],
    "custom_args": {},
    
    "ip": "64.76.21.178",
    "country": "AR",
    "city": "",
​
    "user_agent": "Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.77 Safari/537.36",
    "os_class": "Desktop",
    "os": "Windows NT",
    "os_version": "Windows 7",
    "agent_name_version": "Chrome 70",
    "agent_name": "Chrome"
    
    "url": "",
    "link_id": "",
    "interests": []        
}
```

​Para el caso de `track.mail.clicked`, siempre se tendrá disponible la información de geolocalización y dispositivo.

### Evento `track.mail.unsubscribed`

Además de la información general, se incluye también:

* `reason`: Código asociado a la razón de desuscripción. Los valores posibles son:
  * not\_interested
  * too\_frequent
  * spam\_never\_subscribed
  * spam\_offensive
  * spam\_fbl
  * oneclick

### Evento `track.mail.bounced`

Además de la información general, se incluye también:

* `bounce_type`: Tipo de rebote, puede ser hard o soft.
* `message`: Primeras líneas del mensaje de rebote recibido.

### Evento `track.mail.sent`

No se incluye ninguna información adicional además de la general.

### Evento `track.mail.viewed_online`

No se incluye ninguna información adicional además de la general.

### Evento `track.mail.dropped`

No se incluye ninguna información adicional además de la general.

### Evento `track.mail.shared`

Además de toda la información disponible en `track.mail.opened`, se incluye también:

* `shared_on`: red social en la que el contacto compartió el contenido



