---
description: >-
  En esta sección encontrarás los usos más comunes. Si no encuentras lo que
  buscas, avísanos así podemos agregar más ejemplos útiles.
---

# Usos más frecuentes

Para ver el listado todos los de endpoints disponibles, con todos sus parámetros y opciones visita la [referencia completa de la API](https://perfitapiv2.docs.apiary.io/#)



{% hint style="info" %}
Para simplicidad de los ejemplos, no estamos manejando los errores que pueden producirse al hacer las llamadas a la API. 

En un ambiente productivo es importante capturar los errores de forma adecuada.
{% endhint %}

#### Sobre los ejemplos en Node.js

Para los ejemplos en Node.js utilizaremos la librería [axios](https://github.com/axios/axios), por su simplicidad. Deberás instarla de esta forma:

```bash
npm install axios
```

y luego la puedes incluir así:

```javascript
const axios =  require('axios');
```

## Crear o actualizar contacto en una lista

Este es el uso más frecuente, útil para cargar nuevos contactos desde un desarrollo propio, como un formulario o cualquier otro sistema que necesite crear contactos en Perfit.

Tanto la lista, como los intereses y campos personalizados ya deben haber sido creados previamente. En todos estos casos, vamos a referenciarlos usando su `id`.

**Para crear un contacto, usamos el método POST** y la respuesta nos devuelve la información completa del nuevo contacto.

{% tabs %}
{% tab title="Node.js" %}
```javascript
const axios =  require('axios');

const listId = 123;
const account = 'micuenta';
const apiKey = 'micuenta-123456789023467890';

const axiosConfig = { headers: { Authorization: `Bearer ${apiKey}` } };

const contactData = {
    email: 'test@example.com',
    firstName: 'Nombre', 
    lastName: 'Apellido',
    customFields: [
        {id: 10, value: 'valor campo personalizado 1'},
        {id: 11, value: 'valor campo personalizado 2'}
    ],
    interests: [
        {id: 3}, {id: 5}
    ]
}

axios.post(
    `https://api.myperfit.com/v2/${account}/lists/${listId}/contacts`,
    contactData, 
    axiosConfig
).then(response => {
    const contact = response.data.data;
    console.log('Contacto creado/actualizado', contact);    
}); 
```
{% endtab %}

{% tab title="PHP" %}
```php
<?php

$listId = 123;
$account = 'micuenta';
$apiKey = 'micuenta-123456789023467890';

$response = file_get_contents(
    "https://api.myperfit.com/v2/$account/lists/$listId/contacts" ,
    false,
    stream_context_create(['http'=> [
        'method'=>'POST',
        'header' => "Content-Type: application/json\r\n" .
                    "Authorization: Bearer $apiKey",
        'content' => '{
            "email": "test@example.com",
            "firstName": "Nombre",
            "lastName": "Apellido",
            "customFields": [
                { "id": 12, "value": "valor campo personalizado 1" },
                { "id": 13, "value": "valor campo personalizado 2" }
            ],
            "interests": [{"id": 2}, {"id": 3}]
        }'
    ]])
);

var_dump($response);
```
{% endtab %}

{% tab title="cURL" %}
```bash
curl -X POST \
  https://api.myperfit.com/v2/micuenta/lists/123/contacts \
  -H 'Authorization: micuenta-123456789023467890' \
  -H 'Content-Type: application/json' \
  -d '
{"email": "test@example.com",
"firstName": "Nombre",
"lastName": "Apellido",
"customFields": [
{ "id": 12, "value": "valor campo personalizado 1" },
{ "id": 13, "value": "valor campo personalizado 2" }
],
"interests": [{"id": 2}, {"id": 3}]
}'
```
{% endtab %}
{% endtabs %}

## Modificar un contacto existente

En este caso queremos modificar el nombre y un campo personalizado de un contacto específico. Como ID de contacto podemos utilizar tanto la dirección de email, como su ID numérico, en este caso usaremos el email, que es lo más frecuente.

**Para modificar un contacto, usamos el método PUT**, y nos devuelve sólo la información modificada.

{% tabs %}
{% tab title="Node.js" %}
```javascript
const axios =  require('axios');

const account = 'micuenta';
const apiKey = 'micuenta-123456789023467890';

const axiosConfig = { headers: { Authorization: `Bearer ${apiKey}` } };

const email = 'test@example.com';
const contactData = {
    firstName: 'Nombre', 
    customFields: [
        {id: 10, value: 'valor campo personalizado 1'}
    ]
}

axios.put(
    `https://api.myperfit.com/v2/${account}/contacts/${email}`,
    contactData, 
    axiosConfig
).then(response => {
    const contact = response.data.data;
    console.log('Datos modificados', contact);    
}); 
```
{% endtab %}

{% tab title="PHP" %}
```php
<?php

$account = 'micuenta';
$apiKey = 'micuenta-123456789023467890';
$email = 'test@example.com';

$response = file_get_contents(
    "https://api.myperfit.com/v2/$account/contacts/$email" ,
    false,
    stream_context_create(['http'=> [
        'method'=>'PUT',
        'header' => "Content-Type: application/json\r\n" .
                    "Authorization: Bearer $apiKey",
        'content' => '{
            "firstName": "Nombre",
            "customFields": [
                { "id": 12, "value": "valor campo personalizado 1" }
            ]
        }'
    ]])
);

var_dump($response);
```
{% endtab %}

{% tab title="cURL" %}
```bash
curl -X PUT \
  https://api.myperfit.com/v2/micuenta/contacts/test@example.com \
  -H 'Authorization: micuenta-123456789023467890' \
  -H 'Content-Type: application/json' \
  -d '{"firstName": "Nombre",
"customFields": [{ "id": 12, "value": "valor campo personalizado 1" }]}'
```
{% endtab %}
{% endtabs %}

Si en este ejemplo especificas un array con intereses como hicimos en el primer ejemplo, esos intereses van a pisar a los que ya tenga el contacto. En el siguiente ejemplo veremos como hacer para agregar un interés o lista al contacto sin afectar a los que ya tiene asociados.

## Agregar un interés a un contacto

Este ejemplo permite agregar un interés a un contacto \(también puedes hacer lo mismo con las listas\) sin afectar a los demás intereses que pueda tener asociado.

El interés ya debe existir y necesitas su Id para asociarlo al contacto. En este caso, no es necesario incluir un contenido en el body del PUT.

{% tabs %}
{% tab title="Node.js" %}
```javascript
const axios =  require('axios');

const account = 'micuenta';
const apiKey = 'micuenta-123456789023467890';

const axiosConfig = { headers: { Authorization: `Bearer ${apiKey}` } };

const email = 'test@example.com';
const interestId = 123;

axios.put(
    `https://api.myperfit.com/v2/${account}/contacts/${email}/interests/${interestId}`,
    null, 
    axiosConfig
).then(response => {
    const contact = response.data.data;
    console.log('Datos modificados', contact);    
}); 
```
{% endtab %}

{% tab title="PHP" %}
```php
<?php

$account = 'micuenta';
$apiKey = 'micuenta-123456789023467890';
$email = 'test@example.com';
$interestId = 123;

$response = file_get_contents(
    "https://api.myperfit.com/v2/$account/contacts/$email/interests/$interestId" ,
    false,
    stream_context_create(['http'=> [
        'method'=>'PUT',
        'header' => "Content-Type: application/json\r\n" .
                    "Authorization: Bearer $apiKey"
    ]])
);

var_dump($response);
```
{% endtab %}

{% tab title="cURL" %}
```bash
curl -X PUT \
  https://api.myperfit.com/v2/micuenta/contacts/test@example.com/interests/123 \
  -H 'Authorization: micuenta-123456789023467890' \
  -H 'Content-Type: application/json'
```
{% endtab %}
{% endtabs %}

## Desuscribir a un contacto

Este ejemplo resulta muy útil cuando queremos marcar un contacto en Perfit como desuscripto, para no enviarle más comunicaciones.

{% tabs %}
{% tab title="Node.js" %}
```javascript
const axios =  require('axios');

const account = 'micuenta';
const apiKey = 'micuenta-123456789023467890';

const axiosConfig = { headers: { Authorization: `Bearer ${apiKey}` } };

const email = 'test@example.com';

axios.post(
    `https://api.myperfit.com/v2/${account}/contacts/${email}/unsubscribe`,
    null, 
    axiosConfig
).then(response => {
    const contact = response.data.data;
    console.log('Datos modificados', contact);    
}); 
```
{% endtab %}

{% tab title="PHP" %}
```php
<?php

$account = 'micuenta';
$apiKey = 'micuenta-123456789023467890';
$email = 'test@example.com';

$response = file_get_contents(
    "https://api.myperfit.com/v2/$account/contacts/$email/unsubscribe" ,
    false,
    stream_context_create(['http'=> [
        'method'=>'POST',
        'header' => "Content-Type: application/json\r\n" .
                    "Authorization: Bearer $apiKey"
    ]])
);

var_dump($response);
```
{% endtab %}

{% tab title="cURL" %}
```bash
curl -X POST \
  https://api.myperfit.com/v2/micuenta/contacts/test@example.com/unsubscribe \
  -H 'Authorization: micuenta-123456789023467890' \
  -H 'Content-Type: application/json'
```
{% endtab %}
{% endtabs %}







