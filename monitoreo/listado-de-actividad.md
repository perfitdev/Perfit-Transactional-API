---
description: >-
  Es posible obtener el historial de actividad de todos los envíos de la cuenta.
  Pueden obtener los eventos de cada mail enviado, apertura, click,
  desuscripción, rebote, etc.
---

# Listado de actividad

{% hint style="info" %}
La autenticación a utilizar en este recurso es la misma que se utiliza en [Contacts API](../contacts-api/autenticacion.md). Para obtener el API key de un usuario puedes revisar este artículo.
{% endhint %}

{% api-method method="get" host="https://api.myperfit.com/v2" path="/:account/activity" %}
{% api-method-summary %}
/activity
{% endapi-method-summary %}

{% api-method-description %}
Devuelve un listado de los eventos utilizando los filtros indicados. La estructura de los objetos varía dependiendo del tipo de evento, como se indica en la sección Webhooks.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="account" type="string" required=true %}
Nombre de cuenta
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authentication" type="string" required=true %}
API Key de cuenta en Perfit
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-query-parameters %}
{% api-method-parameter name="filters.track\_type" type="string" required=false %}
Filtrado por tipo de evento, ej:  `track.mail.sent`, `track.mail.opened`, `track.mail.clicked`, ... Dejar vacío para recibir todo los tipos de eventos.
{% endapi-method-parameter %}

{% api-method-parameter name="view" type="string" required=false %}
Formato de salida: `full`\(toda la info disponible\), `default`\(info básica\) o `simple`\(sólo email\).
{% endapi-method-parameter %}

{% api-method-parameter name="filters.timestamp.gtrel" type="string" %}
Fecha relativa de inicio de datos. Ej: `now-1h`, `now-5d`
{% endapi-method-parameter %}

{% api-method-parameter name="filters.timestamp.gt" type="boolean" %}
Fecha absulta de inicio de datos. No puede indicarse en conjunto con gtrel. Ej: `2019-10-17T03:49:14Z`
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
    "paging": {
        "next": "",
        "total": 2,
        "results": 2
    },
    "data": [
        { ... },    
        { ... }        
    ],
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

### Paginado

Para obtener las sucesivas páginas, se debe utilizar el link que aparece en `paging.next`. Si su contenido está vació significa que esa es la última págnia.

