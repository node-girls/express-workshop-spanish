---
description: 'Mini desafío #2'
---

# Capítulo 10: Mostrando tus artículos

{% hint style="info" %}
¡Buen trabajo!

Sécate el sudor - ha llegado el desafío final. ¡Puedes hacerlo! 💥
{% endhint %}

Ya estamos guardando los artículos del blog en el servidor. ¡Es hora de cogerlos y mostrarlos en la página!.

Si miras dentro de `public/script.js`, hay un montón de código JavaScript. No te preocupes por lo que significa el código ahora, sólo piensa que es responsable de mandar un request para obtener\(GET\) los artículos antiguos y mostrarlos en la página debajo de "Recent Posts".

`script.js` trata de cargar los posts antiguos haciendo un request GET. Mira dentro a ver si puedes encontrar algún endpoint útil.

Tu archivo `script.js` quiere recibir el JSON conteniendo tus artículos del blog. ¡Tu trabajo es hacer que pase!

Express tiene un método muy útil llamado `res.sendFile()` que permite mandar fácilmente archivos de vuelta al cliente. Usa este método con tu JSON.

Si todo va bien, ¡deberías tener tu propio CMS! 😍

