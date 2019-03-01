# Artículos individuales

Este paso es opcional, sólo por diversión. Se asume que has terminado con éxito el tutorial.

Podemos hacer nuestro CMS todavía mejor, haciendo posible que se puedan ver los artículos de forma individual. Vamos a ver cómo podemos hacerlo.

### Paso 1 - parámetros URL. <a id="step-1-url-parameters"></a>

No queremos tener que escribir un handler por cada URL en nuestra aplicación. Los parámetros URL de express nos permiten especificar secciones dinámicas en la URL - un espacio para los ID de los artículos del blog o un usuario, por ejemplo. Puedes pensar en ellas como los argumentos de una función que son pasados al servidor. 

Los parámetros URL de Express usan `:` para las partes dinámicas de la URL:

* `/users/:userId` - identifica URLs como `/users/123`, `/users/node-girls`
* `/users/:userId/posts/:postId` - identifica URLs como  `/users/node-girls/posts/node-is-best`

Vamos a añadir otro handler para mostrar artículos individuales del blog.

{% code-tabs %}
{% code-tabs-item title="server.js" %}
```javascript
app.get('/posts/:postId', function (req, res) {    res.send('post id: ' + req.params.postId);});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

¿Qué piensas que vas a ver cuando visites [http://localhost:3000/posts/abc123](http://localhost:3000/posts/abc123) en tu navegador?

### Paso 2 - Leyendo del archivo y mandando el artículo específico <a id="step-2-reading-from-the-file-and-sending-the-specific-blog-post"></a>

Igual que en [`/create-post`](https://github.com/node-girls/express-workshop/blob/master/step08.md#reading-from-your-hard-drive), necesitas leer tu archivo JSON. Prueba y envía el contenido del artículo al navegador con:`res.send(postContentHere)`

### Paso 3 - Renderizando una plantilla <a id="step-3-rendering-a-template"></a>

Ahora mismo estamos mandando texto plano, pero probablemente quieras mostrar tu artículo con HTML y CSS. Pa hacerlo, podemos usar el sistema de plantillas incorporado en Express. Puedes usar cualquier lenguaje de plantillas que quieras \([pug/jade](https://pugjs.org/), [ejs](http://www.embeddedjs.com/), o [handlebars](http://handlebarsjs.com/)\), pero vamos a usar [mustache](https://mustache.github.io/) \(que es muy similar a handlebars\) en este ejemplo.

Ejecuta `npm install --save mustache-express`, después comprueba la documentación para [mustache-express](https://www.npmjs.com/package/mustache-express) y [plantillas de Express](http://expressjs.com/en/guide/using-template-engines.html). Necesitas crear un archivo de plantilla en `views/post.mustache` como este:

{% code-tabs %}
{% code-tabs-item title="views/post.mustache" %}
```javascript
<!DOCTYPE html>
<html>
  <head>
      <title>Blog Post</title>
  </head>
  <body>
      <h1>yay blog post!</h1>
          <article>
            {{ post }}
          </article>
  </body>
</html>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Si te has quedado atascado, mira el [ejemplo de solución](https://github.com/node-girls/express-workshop-complete/tree/templating) :\)

### Todavía más desafíos: <a id="even-more-stretch-goals"></a>

* Añade títulos a tus posts
* Añade un índice
* Renderiza los post con Markdown

