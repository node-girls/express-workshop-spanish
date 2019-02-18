# Capítulo 4: Comunicarse con el servidor

Ahora que hemos construido el servidor, necesitamos comunicarnos con él. Vamos a controlar el servidor con **handler functions**.

## ¿Qué es una handler function?

Cuando una **request** alcanza al servidor, necesitamos una forma de responder a la misma. Ahí es donde entra una **handler function**. Una **handler function** es sólo una función que recibe **requests** y las maneja, de ahí el nombre,

Una **handler function** siempre toma una `request` y un objeto `response`, y manda la respuesta de vuelta al cliente con información. Tú eliges que quieres mandar de vuelta en la **response**.

¿Cómo es una **handler function** en Express?

El método `get()` se usa para definer una **handler function** en Express. Necesita dos parámetros: el **endpoint** que va a disparar la acción \(explicaremos más sobre esto en el siguiente paso\), y la **handler function** que indica exactamente qué hay que hacer. Aquí hay un ejemplo "Hello World":

{% code-tabs %}
{% code-tabs-item title="server.js" %}
```javascript
app.get("/", function (req, res) {
    res.send("Hello World!");
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

En este ejemplo, le decimos a nuestro servidor que responda con "Hello World!" cuando alguien intente acceder a la página web.

### 1. Crea tu propia handler function

Ahora vamos a crear una **handler function** con un mensaje personalizado en nuestra **response**. Puedes escribir el mensaje que tú quieras.

Actualiza tu `server.js` con una función `app.get()` vacía:

{% code-tabs %}
{% code-tabs-item title="server.js" %}
```javascript
var express = require("express");

var app = express();

app.get("/", function (req, res) {

});

app.listen(3000, function () {
  console.log("Server is listening on port 3000. Ready to accept requests!");
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Prueba a hacer `console.log` del objeto `req` dentro de la handler function. Reinicia tu servidor,  recarga el navegador y, después, ve a tu ventana de terminal para ver lo que ocurre. Deberías ver muchos datos aparecer.

### 2. Dile a tu handler function que hacer

Queremos que nuestra **handler function** envíe de vuelta un mensaje al cliente. Para hacer eso, vamos a usar el método de Express `send()`. Esto actualizará el objeto **response** con el mensaje.

Actualiza tu **handler function**:

{% code-tabs %}
{% code-tabs-item title="server.js" %}
```javascript
var express = require("express");
var app = express();

app.get("/", function (req, res) {
  res.send("Yay Node Girls!");
});

app.listen(3000, function () {
  console.log("Server is listening on port 3000. Ready to accept requests!");
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### 3. Compruébalo en tu navegador

Para la ejecución de tu servidor con `Ctrl + C`. Después inícialo de nuevo para ejecutar tus cambios.

{% code-tabs %}
{% code-tabs-item title="Command line" %}
```bash
$ node server.js
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Ahora, abre tu navegador favorito y ve a la url `http://localhost:3000`. Si ver tu mensaje en el navegador, ¡Enhorabuena! Acabas de mandar tu primer **response** desde el servidor.

