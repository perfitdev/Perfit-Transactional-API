---
description: >-
  Este es el uso más frecuente, útil para cargar nuevos contactos desde un
  desarrollo propio, como un formulario o cualquier otro sistema que necesite
  crear contactos en Perfit.
---

# Crear o actualizar un contacto en una lista

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



