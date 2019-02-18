# Capítulo 7: Enviando los artículos de tu blog al servidor

Hasta ahora hemos estado haciendo pidiendo datos a nuestro servidor. Pero también podemos _mandar_ datos al servidor para ser guardado en alguna parte.

## Métodos HTTP request

Todos los requests usando uno de los métodos HTTP. Los principales son: `GET`, `POST`, `PUT`, `PATCH` y `DELETE`.

`app.get` es para los requests que usan el método HTTP `GET`.

### El método HTTP request POST

Cuando mandamos datos al servidor, usamos el método HTTP request `POST`, en vez de `GET`. Para entender la diferencia, ve hacia el enlace "POST vs GET" en la sección del Glosario.

Vamos a probar a mandar texto al servidor por `POST`.

Vamos a añadir un formulario a la página `index.html` , para que puedas escribir los artículos de tu blog desde ahí.

Abre el archivo `index.html` en tu editor de texto. Si le echas un vistazo, verás algo así:

{% code-tabs %}
{% code-tabs-item title="index.html" %}
```markup
<div class="entry-container">
    <!--PASTE YOUR CODE HERE!! -->
</div>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

**Reemplaza la zona comentada con este fragmento de código:**

{% code-tabs %}
{% code-tabs-item title="index.html" %}
```markup
<h3>Create a blog post</h3>
<form action="/create-post" method="POST">
    <textarea name="blogpost" rows="10" cols="14"></textarea>
    <button type="submit">Send</button>
</form>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Vamos a mirar a este formulario un poco más de cerca.

* El formulario tiene un textarea y un botón de enviar.
* El atributo `action` es el endpoint a donde los datos del formulario se van a enviar.
* El atributo `name` será usado más tarde para hacer referencia a los datos.

Cuando pulses enviar, el formulario enviará un request por `POST` al servidor, usando lo que ponga en el atributo `action` como endpoint. En nuestro caso es `/create-post`. En nuestro servidor tenemos que escribir algo de código para manejar con los requests que vengan al endpoint `POST /create-post`. 

## Recibiendo el artículo del blog en el servidor

Los datos no llegan al servidor de una pasada; fluyen al servidor como un **stream**. Piensa en el **stream** como agua fluyendo de un grifo a un cubo.

Si estuviésemos escribiendo un servidor en NodeJs puro, tendríamos que pensar en cómo recolectar el **stream** de forma apropiada. Pero por suerte para nosotras, Express se encarga de manejar todas esas cosas. 

Todo lo que necesitas es definir la ruta que va a manejar las requests que vengan a través del endpoint `/create-post`.

Vamos a recordar como era una ruta `GET` en Express:

{% code-tabs %}
{% code-tabs-item title="server.js" %}
```javascript
app.get('/my-lovely-endpoint', function (req, res) {
    res.send('Hello there!');
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Pero esta vez queremos definir una ruta que maneje una request POST. ¿Qué crees que tienes que cambiar? ¡Experimenta y mira si puedes definir una ruta `POST` para el endpoint `/create-post`!.

Por ahora, haz que tu **handler** `/create-post` haga esto: `console.log('/create-post')`.

{% hint style="info" %}
Si necesitas una pista, pídele a una mentora ayuda o hablar con alguna compañera para ver si podéis hacerlo juntas
{% endhint %}

Si consigues manejar con éxito **requests** al **endpoint** `POST /create-post`, ¡estás lista para pasar al capítulo 8!

