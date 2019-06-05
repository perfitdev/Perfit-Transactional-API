---
description: >-
  Algunos ejemplos de cómo es posible crear personalizaciones utilizando el
  motor de personalización.
---

# Ejemplos

## Valores por defecto

Una de las funciones más útiles es la posibilidad de indicar un valor por defecto para los casos en los que no exista o su valor sea vacío, por ejemplo:

`Hola ${contact.name!"amigo"}`

En cualquiera de los siguientes casos, se utilizaría el valor por defecto:

`{"contact": { "name": "" }}` , `{"contact": {} }` , `{ }`

## Bloque condicional

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

## Iterador

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



