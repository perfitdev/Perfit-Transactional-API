---
description: >-
  Es posible personalizar cada email enviado utilizando la información
  disponible en los objetos substitution. Entre otras cosas, es posible indicar
  valores por defecto y bloques condicionales.
---

# Personalización de contenidos

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

## Ejemplos

### Valores por defecto

Una de las funciones más útiles es la posibilidad de indicar un valor por defecto para los casos en los que no exista o su valor sea vacío, por ejemplo:

`Hola ${contact.name!"amigue"}`

En cualquiera de los siguientes casos, se utilizaría el valor por defecto:

`{"contact": { "name": "" }}` , `{"contact": {} }` , `{ }`

### Bloque condicional

A veces se desea mostrar un bloque sólo si se cumplen ciertas condiciones, esto se puede resolver facilmente de esta forma:

```markup
[#if contact.gender == "M"]
  <!-- Contenido para hombres -->
[#else]
  <!-- Contenido para mujeres -->
[/#if]
```

```markup
[#if product.discount != 0]
  <!-- Producto con descuento -->
[#else]
  <!-- Producto sin descuento -->
[/#if]
```

### Iterador

Es posible recorrer arrays y armar el contenido en base a sus elementos, útil por ejemplo para mostrar productos de un carrito abandonado:

Siendo el modelo en `substitutions`:

```javascript
{
      "products": [ 
            { "title": "Producto 1", "price": "$123.50" },
            { "title": "Producto 2", "price": "$234.60" },            
            { "title": "Producto 2", "price": "$345.70" }            
      ]
}
```

Se puede iterar así:

```markup
[#list products as product]
  Producto: ${product.title}
  Precio: ${product.price}
[/#list]
```



