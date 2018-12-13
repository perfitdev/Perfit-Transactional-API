# Monitoreo y links especiales

## Monitoreo

{% hint style="info" %}
**Todos los eventos de monitoreo están asociados a un `mail_id` único por `recipient`.** 
{% endhint %}

En el caso de que para un elemento `recipient` se incluyan `cc` o `bcc`, todos ellos compartirán el mismo `mail_id` y por ende cualquier acción que realicen \(apertura, click, desuscripción, etc.\) quedará asociada al mismo `mail_id`. 

Para evitar este comportamiento, se debería indicar cada uno como un `recipient` único.

### Activación

La opciones de monitoreo se especifican dentro de la sección `tracking`. En caso de no especificarlas, se activarán por defecto tanto el monitoreo de aperturas como el de clicks.

{% hint style="info" %}
El monitreo de aperturas y clicks están sólo disponibles para el contenido de tipo `html`.
{% endhint %}

### Aperturas

Para el monitoreo de aperturas se incluye un tag `<img>` justo antes de cerrar el body del html, por lo que es necesario que del lado cliente se visualicen las imágenes, en caso contrario no será contabilizada la apertura.

### Clicks

El monitoreo de los clicks se realiza reemplazando todos los enlaces \(sólo los indicados en atributos `href`\) por urls propias de Perfit que luego de contabilizar el click hacen un redirect al destino final.

#### Intereses

Es posible indicar una serie de intereses asociados a un link. Estos intereses serán indicados junto a los eventos `track.mail.clicked`. 

La forma de asociar intereses mediante el atributo html `data-interests`. Es posible indicar más de un interés por link, separados por coma:

```markup
<a href="https://www.mydomain.com/prods/123" data-interests="electro,hogar">Link</a>
```

#### Desactivar monitoreo por link

Es posible desactivar el monitoreo de un link específico usando el atributo `data-track-disabled`.

```markup
<a href="https://www.mydomain.com/prods/123" data-track-disabled>No monitoreado</a>
```

#### Links variables

Existen casos en los que los links contienen partes variables, por ejemplo: `https://www.mydomain.com/prods/${product.id}`. El comportamiento por defecto es asociar los eventos de click a la URL original, antes del reemplazo.

Si lo que se desea es medir los clicks sobre cada URL final, es decir luego del reemplazo, es necesario usar el atributo `data-track-final-url`.

```markup
<a href="https://www.mydomain.com/prods/${product.id}" data-track-final-url>Link final</a>
```

### Google Analytics

Los parámetros utm indicados en `tracking.ganalytics` se incluirán en todos los links que se encuentren \(sólo atributos `href`\). Esto se hace independientemente de la activación del monitoreo de clicks. 

Sólo se incluyen en los links los parámetros utm que tengan un valor definido. En caso de que se encuentren links que ua incluyen alguno de los parámetros indicados, no se pisarán, conservando el valor original.

## Links especiales

Existe algunos códigos de reemplazo que sirve para incluir links especiales.

### Versión online

Es posible incluir un link a la versión online del contenido html, su código es:

```text
${urls.online_version}
```

Una forma de utilizarlo podria ser incluyendo un link en el encabezado:

```markup
<a href="${urls.online_version}">Versión online</a>
```

### Desuscripción

De forma similar, se puede incluir un link a la página de desuscripción, utilizando el código:

```text
${urls.online_version}
```

Por ejemplo:

```markup
<a href="${urls.unsubscribe}">Desuscribirme</a>
```



