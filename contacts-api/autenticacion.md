---
description: >-
  La forma preferida de autenticación es utilizando el API key asociado a un
  usuario de Perfit.
---

# Autenticación

## API key

Cada API key está asociado a un usuario en Perfit, por lo que contará con los mismos permisos que ese usuario.

Todos los llamados a la API deben incluir el header `Authorization: Bearer [APIKEY]`

Por ejemplo:

```text
Authorization: Bearer micuenta-apikey12345678901234567890
```

{% hint style="info" %}
Para obtener el API key de un usuario puedes revisar [este artículo](https://docs.myperfit.com/es/articles/1437451-como-obtener-mi-api-key).
{% endhint %}

{% hint style="danger" %}
**NUNCA se debe incluir el API key en código del lado cliente, como por ejemplo javascript del navegador. Utilizarlo SIEMPRE del lado servidor \(php, java, node, …\)**
{% endhint %}

{% hint style="warning" %}
**Siempre que hagas una integración** **es recomendable crear un usuario dedicado** en Perfit, con los permisos mínimos necesarios para la tareas que necesites realizar. Además, resulta útil en caso  que necesites revocar el acceso en algún momento.
{% endhint %}



