---
description: >-
  Si usaste un API REST alguna vez, vas a sentirte como en casa. Si no, en esta
  guía vas a encontrar todo lo necesario para hacerlo.
---

# Introducción

## Endpoint URLs

Para comunicarnos con el API, debemos hacer un pedido a la **URL base** del API, seguido de la versión de la api \(siempre v2 por ahora\), seguido del nombre de nuestra cuenta y el **namespace** correspondiente, es decir, el nombre del recurso al cual deseamos acceder. 

Los namespaces están en inglés, pero es muy sencillo reconocerlos. Puedes ver un listado completo de los namespaces disponibles en nuestro [listado de llamadas](https://perfitapiv2.docs.apiary.io/).

Por ejemplo, si necesitamos leer información de los contactos, entonces el namespace será `contacts` y la URL completa será algo como:

```text
https://api.myperfit.com/v2/micuenta/contacts
```

## Métodos REST

Para leer o escribir información a través del API debemos hacer pedidos HTTP. Como las convenciones de REST indican, los métodos utilizados son los siguientes:

| Método | URL | Efecto |
| :--- | :--- | :--- |
| **GET** | `/[account]/[namespace]` | Obtener un listado de elementos |
| **GET** | `/[account]/[namespace]/[id]` | Obtener el detalle de un elemento |
| **POST** | `/[account]/[namespace]` | Crear un nuevo elemento |
| **PUT** | `/[account]/[namespace]/[id]` | Modificar un elemento |
| **DELETE** | `/[account]/[namespace]/[id]` | Eliminar un elemento |

Cada namespace funciona como una **colección** de elementos. Cada uno de esos elementos tiene un ID único. 

Al crear un elemento con un POST, el elemento recibe un ID automáticamente. Ese ID nos servirá para luego acceder a sus datos \(GET\), modificarlo \(PUT\) o eliminarlo \(DELETE\) utilizando la URL del namespace seguida del ID del elemento. 

Por ejemplo, si se trata del contacto 21, la URL sería:

```text
https://api.myperfit.com/v2/micuenta/contacts/21
```



