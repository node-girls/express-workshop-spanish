# Capítulo 5: Routing

Ahora mismo nuestro servidor sólo hace una cosa. Cuando recibe una **request** desde el **endpoint** raíz `/`, manda de vuelta la misma response: "Yay Node Girls!".

¿Quieres comprobarlo? Prueba a ir a [http://localhost:3000/nodegirls](http://localhost:3000/nodegirls) y ver que pasa.

A pesar de ello, haciendo uso de los **endpoints**, podemos hacer que el servidor mande diferentes **responses** para diferentes **requests**. Este concepto se denomina **routing**.

## ¿Qué es un endpoint? <a id="what-is-an-endpoint"></a>

Un endpoint es  la parte de una URL que viene justo después de `/`. Por ejemplo `/chocolate` es el **endpoint** "chocolate". Es la URL a la que mandas la request.

### 1. Crea tus propios endpoints y manda diferentes responses <a id="1-create-your-own-endpoints-and-send-different-responses"></a>

Vamos a probar a mandar diferentes **responses** a diferentes **endpoints**. ¿Recuerdas el método `app.get()`? Para montar un routing en tu servidor, sólo necesitamos repetir este método con diferentes **endpoints**.

Por ejemplo:

{% code-tabs %}
{% code-tabs-item title="server.js" %}
```javascript
app.get("/", function (req, res) {
    res.send("Hello World!");
});

​app.get("/chocolate", function (req, res) {
    res.send("Mm chocolate :O");
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

_Desafío:_  Añade código para que tu servidor envíe un mensaje cuando el endpoint sea `/node` y otro para cuando sea `/girls`.

