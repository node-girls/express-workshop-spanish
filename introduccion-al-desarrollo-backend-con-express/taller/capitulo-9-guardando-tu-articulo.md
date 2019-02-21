---
description: 'Mini desafío #1'
---

# Capítulo 9: Guardando tu artículo

{% hint style="info" %}
📣Ha llegado el momento de un mini desafío. Los capítulos 9 y 10 requieren un poco de resolución de problemas. No te preocupes, ¡estos mini desafíos son 100% asumibles con las cosas que has aprendido hasta ahora!

Como siempre, habla con una mentora o trabaja en equipo si lo necesitas.
{% endhint %}

Ahora mismo, tus preciosos artículos no se están guardando en ninguna parte, lo que es un poco embarazoso. Vamos a hacer algo para remediarlo.

## JSON - Un formato de datos práctico <a id="json-the-handy-data-format"></a>

Notarás que en la carpeta "data" hay un archivo nuevo llamado `posts.json`.

JSON es un tipo de archivo para estructurar datos en un formato legible. También es un formato muy popular para mandar datos a través de internet.

JSON es la representación en string\(cadena de texto\) de un objeto Javascript. Los objetos JSON se convierten de forma muy sencilla a objetos javascript, y viceversa, con `JSON.parse()` y `JSON.stringify()`.

\(Si no te sientes segura con los objetos Javascript, habla con tu mentora o con una compañera.\)

Si miras en posts.json verás que ya hay un artículo. El formato es:

{% code-tabs %}
{% code-tabs-item title="posts.json" %}
```javascript
{    [timestamp]: [blog post message]}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Hemos usado **timestamp** como la clave para que los artículos se listen en orden cronológico. También registra la fecha de creación.

## Guardando en tu disco duro <a id="writing-to-your-hard-drive"></a>

Cada vez que un artículo llegue al servidor, queremos almacenar los datos en el disco duro de tu ordenador. Para hacer esto, necesitamos un módulo incorporado en NodeJs: `fs` , file system.

Los módulos incorporados de NodeJs \(módulos del **core**\) son parecidos a las funciones **middleware** incorporadas de express. La única diferencia es que mientras que necesitas tener instalado Express para usar sus funciones **middleware**, las funciones **core** vienen automáticamente con NodeJs.

Para usar `fs`, necesitamos hacer require en tu servidor:

{% code-tabs %}
{% code-tabs-item title="server.js" %}
```javascript
var fs = require('fs');
```
{% endcode-tabs-item %}
{% endcode-tabs %}

El método que necesitamos para escribir en tu disco duro es `fs.writeFile`

{% code-tabs %}
{% code-tabs-item title="server.js" %}
```javascript
fs.writeFile('location-of-your-file-goes-here', yourData, function (error) {    // do something});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Vamos a echar un vistazo más detallado.

`fs.writeFile` usa 3 **argumentos**:

* Argumento 1: La localización del archivo en el que quieres escribir
* Argumento 2: Los datos que quieres escribir
* Argumento 3: la función **callback**

Reemplaza `'location-of-your-file-goes-here'` con la dirección actual del archivo donde quieres escribir. Si no existe, `fs.writeFile`creará uno. Ya tenemos `posts.json`, asi que no hay de qué preocuparse.

## Leyendo tu disco duro <a id="reading-from-your-hard-drive"></a>

Para leer datos que ya existen, usarías `fs.readFile`. La forma en la que usas `fs.readFile` es muy similar a `fs.writeFile`

{% code-tabs %}
{% code-tabs-item title="server.js" %}
```javascript
fs.readFile('location-of-your-file-goes-here', function (error, file) {    // do something});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

* Argumento 1: La localización del archivo en el que quieres leer
* Argumento 2: la función **callback**

Habrás notado que ls función de callback de  `fs.readFile`tiene un segundo argumento, archivo`file`. Ese argumento es el archivo que quieres leer.

Vamos a leer los datos de `posts.json`. Asegúrate de hacer `require` de `fs`.

Añade este código a tu servidor \(debajo de los `require`\)

{% code-tabs %}
{% code-tabs-item title="server.js" %}
```javascript
fs.readFile(__dirname + '/data/posts.json', function (error, file) {    console.log(file);});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

`__dirname` es un objeto global de Node que te da la ruta a tu directorio raíz actual. es útil cuando queremos evitar escribir rutas dinámicas o largas.

Si reinicias el servidor deberias ver algo así:

{% code-tabs %}
{% code-tabs-item title="command line" %}
```text
<Buffer 7b 0a 20 20 20 20 22 31 34 36 37 33 39 30 33 35 36 32 39 31 22 3a 20 22 54 68 69 73 20 69 73 20 6d 79 20 76 65 72 79 20 66 69 72 73 74 20 62 6c 6f 67 ... >
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Este es el contenido de `posts.json` , pero en un formato llamado buffer. Para hacerlo legible para los humanos, vamos a convertirlo a string:

{% code-tabs %}
{% code-tabs-item title="server.js" %}
```javascript
console.log(file.toString());
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Convertir un JSON a un objeto Javascript <a id="converting-from-json-to-javascript-object"></a>

El archivo`file` está en formato JSON ahora mismo. Si queremos acceder a los artículos que se encuentran dentro del mismo, necesitamos convertirlo de formato JSON a un objeto de Javascript.

Añade este fragmento de código en tu función callback `fs.readFile`.

{% code-tabs %}
{% code-tabs-item title="server.js" %}
```javascript
var parsedFile = JSON.parse(file);
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Ahora la variable parsedFile es un objeto normal de JavaScript, y podemos acceder a los datos que hay dentro.

## Mini desafío <a id="mini-challenge"></a>

Hemos hablado de JSON y hemos hablado sobre cómo leer y escribir archivos. ¡Ahora tienes los poderes para salvar nuevos artículos a tu disco duro! Trabaja en equipo y con una mentora para ver si puedes hacer los siguientes pasos tú sola.

Aquí tienes una guía de lo que tienes que conseguir:

1. Cuando los datos de un artículo nuevo lleguen, lee `posts.json` para acceder a su contenido.
2. Añade tu nuevo artículo junto a los demás. Para cada artículo, usa un timestamp como la clave, y los datos como el valor.
3. Escribe los datos combinados de vuelta al archivo `posts.json`.

#### **Cosas a recordar** <a id="things-to-remember"></a>

`fs.writeFile()` normalmente sobreescribe el archivo con los datos que le pases. Es probable que no quieras perder todos tus datos antiguos cada vez que llegue uno nuevo, asi que piensa en como combinar `fs.readFile()` y `fs.writeFile()`para prevenir la sobreescritura.

Necesitarás convertir varias veces de JSON a JavaScript y viceversa. `JSON.parse()` convierte de JSON a objetos Javascript. `JSON.stringify()` hace el opuesto. Úsalos para el desafío.

Ah, para obtener un timestamp del momento actual, usa el método de JavaScript `Date.now()`

**¡Buena suerte! Cuando acabes avanza al paso 10.**

