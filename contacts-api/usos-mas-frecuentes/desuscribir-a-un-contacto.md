---
description: >-
  Este ejemplo resulta muy útil cuando queremos marcar un contacto en Perfit
  como desuscripto, para no enviarle más comunicaciones.
---

# Desuscribir a un contacto

{% hint style="info" %}
Una vez que el contacto es marcado como desuscripto no se le enviarán más emails. Esta acción no puede revertirse, la única forma es que el mismo contacto se re-suscriba a través de un formulario optin.
{% endhint %}

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







