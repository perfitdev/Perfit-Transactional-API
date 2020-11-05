---
description: >-
  En este caso queremos modificar el nombre y un campo personalizado de un
  contacto específico.
---

# Modificar un contacto existente

Como ID de contacto podemos utilizar tanto la dirección de email, como su ID numérico, en este caso usaremos el email, que es lo más frecuente.

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



