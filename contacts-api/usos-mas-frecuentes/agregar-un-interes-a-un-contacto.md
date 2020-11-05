---
description: >-
  Este ejemplo permite agregar un interés a un contacto (también puedes hacer lo
  mismo con las listas) sin afectar a los demás intereses que pueda tener
  asociado.
---

# Agregar un interés a un contacto

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



