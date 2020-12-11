---
description: >-
  Es posible personalizar cada email enviado utilizando la información
  disponible en los objetos substitution. Entre otras cosas, es posible indicar
  valores por defecto y bloques condicionales.
---

# Contenidos dinámicos

{% hint style="success" %}
Cuando se desea enviar una gran número de emails con un contenido similar, siempre que sea posible, es conveniente agrupar muchos `recipients` en un mismo POST y utilizar la personalización del contenido,  en vez de enviar un mensaje individial para cada uno.  **Esto mejor notablemente la performance y velocidad de entrega.**
{% endhint %}

## Personalización por destinatario

**El procesamiento del contenido se realiza por cada elemento `recipient`.** Esto implica que si para un mismo`recipient` se indican otros destintarios de tipo `cc` o `bcc`, estos recibirán **exactamente la misma copia del contenido.** 

Si se desea evitar este comportamiento, se deberán utilizar recipients independientes para cada destinatario.

## Motor de personalización

Utilizamos [Free Marker](https://freemarker.apache.org/) como motor de reemplazo, por lo que es posible utilizar todas las directivas y built-ins disponibles en su [documentación](https://freemarker.apache.org/docs/ref.html).

Es importante tener en cuenta que se debe utilizar la notación con corchetes para las directivas, por ejemplo:`[#if test] ... [/#if]`

Es posible utilizar los códigos de reemplazo en los siguientes elementos:

* `subject`
* `content.html`
* `content.text`
* `headers.value`

## Precedencia de modelos

Todos los objetos indicados dentro de `substitution`, tanto a nivel general como a nivel de `recipient`, pueden ser accedidos desde los contenidos. 

En caso de que un mismo objeto esté definido tanto a nivel de recipient como a nivel general, **tendrá siempre precedencia el definido a nivel de recipient**, es decir, el valor del `recipient` "pisa" al valor general.



