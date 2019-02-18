# Capítulo 6: Servir archivos estáticos

Sabemos como mandar un mensaje simple. Pero ¿qué pasa si quieres enviar de vuelta una página HTML, o una imagen?

Algunas cosas como los archivos HTML, imágenes, etc son conocidos como **assets estáticos**. Si deseas que tu servidor "sirva" **assets estáticos** de vuelta al navegador, necesitas hacer algo diferente que sólo usar el método `res.send()`.

Para ser capaz de mandar cualquier archivo desde el servidor necesitamos una función **middleware** incorporada en Express: `express.static()`. Puedes leer más sobre ella [aquí](http://expressjs.com/en/starter/static-files.html) \(en inglés\).

Digamos que queremos servir todos los assets estáticos en nuestra carpeta `public`. La función `express.static()` se vería más o menos así:

{% code-tabs %}
{% code-tabs-item title="server.js" %}
```javascript
app.use(express.static("public"));
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Servir archivos estáticos desde tu servidor

Borra todas tus funciones endpoint `app.get`, y reemplázalas con la línea de código anterior. Reinicia tu servidor, recarga tu navegador y ¡mira lo que pasa! Si ves un CMS de Node Girls, entonces tus assets estáticos se han servido correctamente.

