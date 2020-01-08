---
description: Puedes realizar envíos transaccionales desde PHP usando cURL
---

# Ejemplo en PHP

## Uso básico

```php
<?php

$data = '{
    "from": { "email": "remitente@example.com" },
    "subject": "Asunto de prueba",
    "content": {"html": "<h1>Funciona!</h1>"},
    "recipients": [{"to": {"email": "recipient@example.com"}}]
}';

$ch = curl_init('https://transactional.myperfit.com/v1/mail/send');
curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "POST");
curl_setopt($ch, CURLOPT_POSTFIELDS, $data);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_HTTPHEADER, array(
    "Authorization: Bearer API_KEY",
    "Content-Type: application/json"
));

$result = curl_exec($ch);
```

