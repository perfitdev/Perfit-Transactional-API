---
description: Algunos ejemplos básicos para usar como referencia.
---

# Ejemplos PHP y Node

## PHP

Ejemplo básico en PHP usando la libraría cURL

```php
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

## Node.js

Un ejemplo sencillo usando la libraría [axios](https://github.com/axios/axios).

```javascript
const axiosConfig = {
    headers: { 'Authorization': `Bearer ${transactionalApiKey}` }
}

const postData = {
    from: { email: 'remitente@example.com' },
    subject: 'Asunto de prueba',
    recipients: [
        { to: { email: 'recipient@example.com' } }
    ],
    content: { html: '<h1>Funciona!</h1>}
}

await axios.post('https://transactional.myperfit.com/v1/mail/send ', 
    postData, 
    axiosConfig);
```



