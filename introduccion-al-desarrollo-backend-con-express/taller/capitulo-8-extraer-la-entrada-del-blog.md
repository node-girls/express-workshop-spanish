# Capítulo 8: Extraer la entrada del blog

Ahora tenemos un handler para /create-post. El siguiente paso es encontrar nuestra entrada del blog.

Los contenidos de tu entrada del blog están ocultos en tu objeto `req` en alguna parte. Normalmente lo extraerías de `req.body`. Haz un `console.log` de `req.body` ahora.

¿Recibes un `undefined`? No te preocupes, es normal. Cuando los datos se han mandado por `POST` al servidor en forma de `FormData` \(datos enviados a través del formulario\), tenemos que hacer el proceso de forma un poco diferente para acceder a los datos que llegan a través del `request`.

Necesitamos otra función **middleware**. Algo que permita la extracción de los contenidos del objeto especial `FormData`. Para esto usaremos `express-formidable`. `express-formidable` es otro middleware de Express. Extraerá los datos del formulario del request y hará que estén disponibles para ti cuando hagas `req.fields`.

Esta vez, `express-formidable` no está incorporado, tenemos que instalarlo.

## **Instalando `express-formidable`**

Ve a tu ventana de terminal y desde la raíz del proyecto instala express-formidable:

{% code-tabs %}
{% code-tabs-item title="Command line" %}
```bash
npm install express-formidable --save
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Después, tienes que hacer `require` a la librería `express-formidable` para poder usarla en tu código. No puedes usar guiones en los nombres de variables en Javascript, así que vamos a llamarlo `formidable` a secas. Hazle **require** en la parte superior del código del archivo `server.js`. Normalmente los require es buena práctica requerirlos al principio del documento antes de declarar o programar nada más.

{% code-tabs %}
{% code-tabs-item title="server.js" %}
```javascript
var formidable = require('express-formidable');
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Ahora en algún lugar entre los `require` y tu endpoint `/create-post`, añade la siguiente línea:

{% code-tabs %}
{% code-tabs-item title="server.js" %}
```javascript
// require stuff above

app.use(formidable());

// endpoint stuff below
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Por último dentro del endpoint `/create-post`, añade:

{% code-tabs %}
{% code-tabs-item title="server.js" %}
```javascript
console.log(req.fields);
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Actualiza tu servidor e intenta de nuevo mandar un artículo para el blog.

Ahora deberías ver un objeto en tu consola. La **key** \(clave\) debería ser `blogpost`, como el atributo `name` del formulario. ¡El valor de `blogpost` debería ser tu mensaje!

