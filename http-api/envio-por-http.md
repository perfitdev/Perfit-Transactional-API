---
description: >-
  La API HTTP permite enviar un contenido a uno o varios destinatarios con un
  sólo POST, utilizar variables de reemplazo para personalizarlos, e incluir
  etiquetas y atributos para su seguimiento.
---

# Envío a través HTTP

## Ejemplo básico

Empecemos por el ejemplo más sencillo posible:

```bash
curl -X POST \
  https://transactional.myperfit.com/v1/mail/send \
  -H 'Authorization: <<MI_API_KEY>>' \
  -H 'Content-Type: application/json' \
  -d '{
    "from": { "email": "remitente@example.com" },
    "subject": "Asunto de prueba",
    "content": {"html": "<h1>Funciona! 💪</h1>"},
    "recipients": [{"to": {"email": "recipient@example.com"}}]
}'
```

## Ejemplo usando una plantilla

Otra forma de indicar el contenido es utilizando una plantilla diseñada en la aplicación web, donde ya incluyen el remitente asunto y contenido.

```bash
curl -X POST \
  https://transactional.myperfit.com/v1/mail/send \
  -H 'Authorization: <<MI_API_KEY>>' \
  -H 'Content-Type: application/json' \
  -d '{
    "template_id": "etpl_efd23wnfo23edsoirsnde",
    "recipients": [{"to": {"email": "recipient@example.com"}}]
}'
```

{% api-method method="post" host="https://transactional.myperfit.com/v1" path="/mail/send" %}
{% api-method-summary %}
/mail/send
{% endapi-method-summary %}

{% api-method-description %}
Este endpoint permite encolar para su envío uno o varios emails que compartan el mismo contenido.   
  
Es posible enviar a hasta 1000 destinatarios \(`recipients`\) en un mismo request.  
  
El `content`,  `subject` y `headers` pueden ser personalizados utilizando etiquetas de reemplazo del estilo `${object.key}`.    
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Bearer &lt;&lt;API-KEY&gt;&gt;
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="Body" type="object" required=true %}
Cuerpo del mensaje en formato JSON
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

### Estructura del mensaje

Los únicos parámetros requeridos del body son: **`from.email`**, **`subject`**, **`content`** \(al menos uno: `html` o `text`\) y **`recipients`** \(al menos uno, incluyendo al menos **`to.email`**\).

* **`from`**: **Object, requerido**. **Email y nombre del remitente.**
  * **`email`**: **String, requerido**.
  * `name`: String, opcional.
* `reply_to`: Object, opcional. Dirección y nombre de respuesta.
  * `email`: String, requerido.
  * `name`: String, opcional.
* **`subject`**: **String, requerido, max 200 chars. Asunto del correo.**
* **`content`**: **Object, requerido**. **Se debe indicar al menos un tipo.**
  * `html`: String, opcional, max 300KB. Contenido de tipo `text/html`. 
  * `text`: String, opcional, max 300KB. Contenido de tipo `text/plain`.
* **`template_id`: String, opcional. El id de la plantilla a utilizar.** En caso de usar una plantilla, dejan de ser requeridos los campos from, reply\_to, subject y content, y sus valores serán ignorados en caso de estar presentes.
* `headers`: Object, opcional. Mapa string-string con headers adicionales a incluir.
* **`recipients`: Array de objetos, requerido**. **Debe contener al menos un elemento.**
  * **`to`**: **Object, requerido. Email y nombre del destinatario.**
    * **`email`**: **String, requerido**.
    * `name`: String, opcional.
  * `cc`: Array de objects, opcional. Listado de destinatarios en copia.
    * `email`: String, requerido.
    * `name`: String, opcional
  * `bcc`: Array de objects, opcional. Misma estructura que el cc. Listado de destinatarios en copia oculta.
  * `substitutions`: Object, opcional. Modelo de reemplazo asociado a este destinatario.
  * `custom_args`: Object, opcional. Mapa string-string con información de identificación y seguimiento. Se informarán junto con los eventos de monitoreo.
  * `tags`: Array de strings, opcional. Etiquetas de identificación y seguimiento de este batch. Se informarán junto con los eventos de monitoreo.
* `substitutions`: Object, opcional. Modelo de reemplazo asociado a todo el batch.
* `tracking`: Object, opcional.
  * `open`: Object, opcional.
    * `enable`: Boolean, opcional, default: `true`. Activar monitoreo de aperturas.
  * `click`: Object, opcional.
    * `enable`: Boolean, opcional, default: `true` Activar monitoreo de clicks.
  * `ganalytics`: Object, opcional. Códigos de seguimiento para Google Analytics.
    * `utm_source`: String, opcional.
    * `utm_medium`: String, opcional.
    * `utm_campaign`: String, opcional.
    * `utm_content`: String, opcional.
    * `utm_term`: String, opcional.
* `batch_code`: String, opcional. Identificador alfanumérico \(se limpan todos los caracteres que no sean \[a-z0-9\]\). 
* `tags`: Array de strings, opcional. Etiquetas de identificación y seguimiento de este batch. Se informarán junto con los eventos de monitoreo. 
* `launch_date`: Fecha. Posponer el envío de este batch hasta la fecha y hora indicadas. Si no se indica se envía en forma inmediata.

Este objeto JSON incluye todas las opciones mencionadas.

```javascript
{
	"from": {
		"email": "diego@perfit.com.ar", 
		"name": "Diego"
	},
	"reply_to": {
		"email": "soporte@myperfit.com", 
		"name": "Diego"
	},
	"subject": "Hola ${contact.first_name}, este es el asunto",
	"content": {
		"html": "<!DOCTYPE ...><html><body><h1>Hola mundo!</h1></body></html>",
		"text": "Contenido de tipo texto"
	},
	"headers": {
		"X-My-Header": "my custom header value" 
	},
	"recipients" : [
		{
			"to": { 
				"email": "rcpt@example.com",
				"name": "Nombre Recipient"
			},
			"cc": [ 
				{ 
					"email": "cc1@example.com",
					"name": "Nombre CC1"
				},
				{ 
					"email": "cc2@example.com",
					"name": "Nombre CC2"
				}				
			],
			"bcc": [ 
				{ 
					"email": "bcc1@example.com",
					"name": "Nombre BCC1"
				},
				{ 
					"email": "bcc2@example.com",
					"name": "Nombre BCC2"
				},				
			],
			"substitutions": {
				"contact": {
					"email": "diego@myperfit.com",
					"name": "Diego",
					"gender": "M",
					"age": 35,
					"ciudad": "Buenos Aires",
				}
			},
			"custom_args": {
				"internal_id": "43231312",
				"other_attr": "1234"
			},
			"tags": ["cliente frecuente"]
		}
	],
	"substitutions": {
		"account": {
			"business_name": "Perfit",
			"address": "San Nicolas 3940, CABA, Argentina",
		}
	},
	"tracking": { 
		"open": { 
			"enable": true 
		},
		"click": { 
			"enable": true
		},
		"ganalytics": {
			"utm_source": "Perfit",
			"utm_medium": "email",
			"utm_campaign": "my campaign"
		}
	},
	"batch_code": "mycampaign1234",
	"tags": ["electro"],
	"launch_date": "2019-08-20T13:30:00Z",
}

```

{% hint style="success" %}
Cuando es necesario hacer un gran número de requests, es altamente recomendable **mantener las conexiones HTTP abiertas usando keep-alive**. Esto evita todo el overhead que se introduce al establecer las conecciones TCP. En las pruebas realizadas se vieron incrementos de ~5x en los requests por segundo alcanzados.
{% endhint %}





