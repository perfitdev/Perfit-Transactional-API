# Autenticación

{% hint style="info" %}
El API key utilizada para envíos transaccionales **es una API key específica**, distinta a la asociada a cada usuario.

Es fácil identificar sin un API key es para uso de envíos transaccionales, si contiene `tr` luego del nombre de cuenta:

`micuenta-tr-aDsffD35eSdfsadsGFdFfssfsaADS`
{% endhint %}

## Authorization header 

La autenticación se realiza agregando el header `Authorization` a cada request: 

```text
Authorization: Bearer MI_API_KEY
```

#### Por ejemplo:

```text
Authorization: Bearer micuenta-tr-aDsffD35eSdfsadsGFdFfssfsaADS
```

{% hint style="danger" %}
**NUNCA se debe incluir el API key en código del lado cliente, como por ejemplo javascript del navegador. Utilizarlo SIEMPRE del lado servidor \(php, java, node, …\)**
{% endhint %}

{% hint style="info" %}
Puedes generar tu API keys desde la sección Integraciones de tu cuenta de Perfit. Si tienes dudas sobre cómo hacerlo contáctanos a [soporte@myperfit.com](mailto:soporte@myperfit.com).
{% endhint %}



