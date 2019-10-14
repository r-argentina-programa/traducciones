Artículo original: https://blog.logrocket.com/how-browser-rendering-works-behind-the-scenes-6782b0e8fb10/

# Cómo funciona el renderizado del navegador -detrás de escenas

<img src="https://i0.wp.com/storage.googleapis.com/blog-images-backup/1*VmD21Exnic6eQxj5xGrA-Q.png?resize=3812%2C1958&ssl=1" />

El propósito de este artículo es explicar, en términos muy simples, los pasos que toma tu navegador para convertir HTML, CSS y JavaScript en un sitio web funcional con el que puedes interactuar.
 
Conocer el proceso que sigue tu navegador para darle vida a los sitios web te dará habilidades para optimizar tus aplicaciones web para darles más velocidad y rendimiento.
Si estás listo, empecemos.


## Introducción

Cómo renderiza un sitio web un navegador?

Desconstruiremos el proceso en breve, pero primero, es importante repasar algunos conceptos básicos.
Un navegador web es una pieza de software que carga archivos desde un servidor remoto (o tal vez un disco duro) y te los muestra – así permitiendo la interacción con el usuario.

Sé que ya sabes lo que es un navegador :].

De todas maneras, dentro de un navegador existe una pieza de software llamada motor de renderizado.

En el interior de distintos navegadores, hay una parte del navegador que descifra qué mostrar, basado en los archivos que recibe. A esto se le llama motor de renderizado.

El motor de renderizado es un componente fundamental de cada navegador, y cada empresa que desarrolla un navegador llama a sus motores por diferentes nombres.

El motor de Firefox se llama Gecko, y el de Chrome se llama Blink, que está basado en el proyecto WebKit. No dejes que los nombres te confundan. Son solo eso. Nombres. Nada serio.

## Enviando y recibiendo información

Esto no deberia ser una clase de Ciencias de la Computación, pero deberias recordar que los datos se envian a través de internet como 'paquetes' con tamaño medido en bytes.

<img src="https://i1.wp.com/storage.googleapis.com/blog-images-backup/1*rTbp2SJxvoQyKSIA6TGHEw.png?ssl=1" />

El punto al que queremos llegar es que cuando escribes HTML, CSS y JS, y tratas de abrir el archivo HTML En tu navegador, el navegador lee los bytes de HTML desde tu disco duro (o red).

<img src="https://i1.wp.com/storage.googleapis.com/blog-images-backup/1*GSw1oqEpbPo0NmwG_73bPw.png?ssl=1" />

Entendieron? El navegador lee los bytes de datos, y no los caracteres de código que escribieron.
El navegador recibe los bytes de datos, pero en realidad no puede hacer nada con eso. 
Los bytes de datos deben ser convertidos a una forma que el navegador pueda entender. Éste es el primer paso.

<img src="https://i2.wp.com/storage.googleapis.com/blog-images-backup/1*Ib2Ufggiy67xg02Jp8CYhQ.png?ssl=1" />

### De bytes de HTML a DOM
Lo que necesita el navegador para trabajar es un Document Object Model(DOM) (un objeto). 
Entonces, cómo se deriva el objeto DOM? Muy simple.
 
Primero, los bytes de datos se convierten en caracteres. 

<img src="https://i0.wp.com/storage.googleapis.com/blog-images-backup/1*YdURVl_Qkxv9Lf4Ja583-w.png?ssl=1" />

Deberías ver esto en los caracteres de codigo que hayas escrito. La conversión es hecha basada en la codificación de caracteres del archivo HTML. 
En este punto, el navegador fue de bytes de datos a los caracteres reales en el archivo. 
Los caracteres son geniales, pero no son el resultado final. 
Esos caracteres luego son analizados y convertidos en algo llamado tokens. 

<img src="https://i1.wp.com/storage.googleapis.com/blog-images-backup/1*23wqjUorWI2fkCJ_AN5a2w.png?ssl=1" />

Entonces, qué son esos tokens?

Un montón de caracteres en un archivo de texto no le hace mucho bien al motor de renderizado de nuestro navegador.
Sin este proceso de 'tokenización', ese montón de caracteres solo resultaría en un montón de texto sin sentido (o sea, código HTML) que no produce un sitio web real.
Cuando guardas un archivo con la extensión .html, le das una señal al motor de tu navegador para que interprete el archivo como un documento HTML. La manera en la que el navegador «interpreta» este archivo es analizándolo, en primer lugar.
En el proceso de análisis, y particularmente durante la tokenización, se reconocen los inicios y finales de las etiquetas html presentes en el archivo.
Un «parser»(Una parte del navegador que analiza el texto y la estructura de nuestro archivo html) entiende cada cadena de texto entre corchetes(por ejemplo: «<html>», «<p>, y entiende el conjunto de reglas que aplican a cada uno de ellos.
Por ejemplo, un token que representa una etiqueta con un link, tendrá propiedades distintas del que representa una etiqueta con un párrafo. 
Conceptualmente, puedes ver un token como una especie de estructura de datos que contiene información sobre cierta etiqueta html. Esencialmente, un archivo html se puede dividir en pequeñas unidades de análisis llamadas tokens. De esta manera el navegador empieza a entender lo que acabás de escribir.

<img src="https://i0.wp.com/storage.googleapis.com/blog-images-backup/1*vIwWeznQhir5EPWDOyo5sw.png?ssl=1" />

Los tokens son geniales, pero tampoco son nuestro resultado final.

Después de que la 'tokenización” está completa, los tokens son después transformados en nodos.
Podés pensar en los nodos como objetos distintos entre sí con propiedades específicas. De hecho, una mejor manera de explicar esto es ver un nodo como una entidad separada en el interior del árbol de objetos del documento.
Los nodos son geniales, pero todavía no son el resultado final.
Ahora, acá está la última parte.
Una vez creados esos nodos, los mismos son entonces enlazados en una estructura de datos en árbol conocida como el DOM.
El DOM establece las relaciones padre-hijo, y las relaciones 'hermanas' adjacentes.
La relación entre cada nodo es establecida en este objeto DOM.
Ahora, esto es algo con lo que podemos trabajar.

<img src="https://i1.wp.com/storage.googleapis.com/blog-images-backup/1*ugZgXZkxbzeIia7Z3jP76A.png?ssl=1" />

Si te acordás de algo de diseño web básico, sabés que no abrís un archivo CSS o JS en el navegador para ver una página web. No. Abrís el archivo HTML, el cual la mayoría de las veces está en la forma de index.html.
Esta es la razón por la cual tenés que hacer esto: El navegador tiene que pasar por el proceso de transformación de los bytes del archivo .html Al DOM antes de que cualquier cosa suceda.

<img src="https://i2.wp.com/storage.googleapis.com/blog-images-backup/1*Llo-v3XG_gEP_Xlgy0qtjg.png?ssl=1" />

Dependiendo de qué tan grande sea el archivo .HTML, el proceso de construcción del DOM puede tardar algo de tiempo. No importa qué tan pequeño, toma algo de tiempo, sin importar el tamaño de archivo.

<img src="https://i0.wp.com/storage.googleapis.com/blog-images-backup/1*ROuUBS5eZ1DKk2RnFDfh6Q.png?ssl=1" /> 

## Pero esperen. Qué hay de CSS?
El DOM ha sido creado. Genial.
Un archivo .html con un poco de CSS tendría la tabla de estilo enlazada como se muestra abajo:

```html
<!DOCTYPE html>
<html>
<head>
    <link rel="stylesheet" type="text/css" media="screen" href="main.css" />
</head>
<body>
    
</body>
</html>
```

Mientras el navegador recibe los bytes de datos y realiza el proceso de construcción de DOM, tambien hará una petición para recibir la tabla de estilos main.css enlazada.
Tan pronto como el navegador comience a analizar el .html, busca una etiqueta link a un archivo .css, y hace una peticion para recibir el archivo, todo casi en simultáneo.
Como habrás supuesto, el navegador tambien recibe los datos del archivo css en bytes sin procesar, ya sea de internet o de tu disco local.
Pero qué exactamente se hace con esos bytes sin procesar de datos CSS?


## De bytes sin procesar de CSS a CSSOM
Verán, un proceso similar al de los bytes sin procesar de HTML es también iniciado cuando el navegador recibe bytes sin procesar de CSS.
Y con eso me refiero a que, los bytes sin procesar son convertidos a caracteres, después tokenizados, y también se forman nodos, y finalmente, una estructura de árbol también se forma.
Qué es una estructura de árbol?
Bien, la mayoría de las personas saben que existe algo llamado el DOM. De la misma manera, también hay una estructura CSS en forma de árbol llamada el «CSS Object Model», o CSSOM como abreviatura.
Verán, el navegador no puede trabajar con bytes sin procesar de HTML o CSS. Esto debe ser convertido a una forma que pueda reconocer -las estructuras de árbol.

<img src="https://i0.wp.com/storage.googleapis.com/blog-images-backup/1*5GYEa442MdwmhPGJbGagGw.png?ssl=1" />

CSS tiene algo llamado la «Cascada». La Cascada es como el navegador determina qué estilos son aplicados a un elemento.
Debiéndose al hecho de que los estilos afectando a un elemento pueden venir de un elemento padre(herencia), o pueden estar configurados en el mismo elemento, la estructura de árbol CSSOM se vuelve importante.
¿Por qué?
Esto es porque el navegador tiene que recorrer recursivamente a través de la estructura del árbol CSS y determinar los elementos que afectan a un elemento en particular.
Todo bien hasta acá, todo funciona perfecto.
El navegador tiene los objetos DOM y CSSOM. Podemos tener algo renderizado a la pantalla ahora?


## El árbol de renderizado


Lo que tenemos hasta ahora son dos estructuras independientes en forma de árbol, que al parecer, no tienen un objetivo en común.

<img src="https://i1.wp.com/storage.googleapis.com/blog-images-backup/1*uqHMI5h_gcrycAXgwnq8hw.png?ssl=1" />

Las estructuras en forma de árbol: DOM y CSSOM, son dos estructuras independientes.

El DOM contiene toda la información correspondiente a la relación que existe entre los elementos HTML de una página web, mientras que el CSSOM contiene información relacionada a como estos elementos reciben un estilo.

Lo que sucede luego, es que el navegador combina las estructuras en forma de árbol: DOM y CSSOM, dando como resultado algo llamado El árbol de renderizado.

<img src="https://i2.wp.com/storage.googleapis.com/blog-images-backup/1*10ytkQcfKdbfGQxvYj2-5A.png?ssl=1" />

El árbol de renderizado contiene toda la información visible del contenido DOM de una página web y, contiene toda la información CSSOM requerida por los diferentes nodos.

Notesé que, si un elemento ha sido escondido por la propiedad CSS, “display: none;”, ese nodo no será representado en el árbol de renderizado.

El elemento escondido estará presente en el DOM pero no en el árbol de renderizado.

La rázon por la cual esto sucede, es debido a que el árbol de renderizado combina información tanto del DOM como del CSSOM, por lo tanto, sabe que no debe incluir un elemento escondido en el árbol.

## Coloquemos los elementos

Con el árbol de renderizado ya construido, el siguiente paso es colocar los elementos en la página web.

En este momento, se tiene información del contenido visible en la pantalla, tanto los elementos HTML como sus correspondientes estilos, pero, todavía no hemos renderizado nada en la pantalla.

Esto se debe a que, primero, el navegador debe calcular el tamaño y la posición exacta de cada objeto en la página web.

Para ilustrar de manera sencilla esto, deben imaginarse que están pasando todo el contenido HTML con su estilo correspondiente a un matematico talentoso el cual se encargará de renderizar la página. Este matematico determina con exactitud el tamaño y la posición en cada elemento visible del navegador.

<img src="https://i0.wp.com/storage.googleapis.com/blog-images-backup/1*MMJ5DCdRhZMdy8K7CFAsZw.png?ssl=1" />

Asombroso, no?

Este proceso de colocar todos los elementos en el navegador considera todo el contenido y los estilos recibidos por el DOM y el CSSOM para poder realizar la colocación correcta.

A veces, escucharas que este proceso de colocar los elementos, también recibe el nombre de “reflow”.



## Deja salir al artista

Con toda la información de las posiciones exactas de cada elemento, lo único que queda por hacer es “pintar” los elementos en la pantalla.

Piensa en esto por un momento. Tenemos toda la información requerida para mostrar los elementos en la pantalla. Lo único que debemos hacer ahora es mostrársela al usuario,no?

Si, es exactamente de lo que trata este proceso!.

Con la información de los elementos HTML (DOM), estilo (CSSOM), y como exactamente cada uno de esos elementos es colocado en pantalla (posición y tamaño), el navegador “pinta” el nodo individual en la pantalla.

Finalmente, todos los elementos han sido renderizados en la pantalla.



## Recursos que previenen el renderizado

Cuando lees “prevenir el renderizado”, que se te viene a la mente?

Bueno, si tengo que adivinar: “Algo que previene el “pintado” de los nodos en la pantalla”.

Si has dicho eso, estas en lo cierto!.

La primera regla para optimizar tu sitio web es la de: cargar los elementos más importantes de HTML y CSS al cliente, tan rapido como sea posible.

Tanto el DOM como el CSSOM deben ser construidos antes de un “pintado” exitoso, por lo tanto, ambos, el HTML y el CSS son recursos que previenen el renderizado.

El punto es: para optimizar el tiempo del primer renderizado de tus aplicaciones lo que deberías hacer es cargar tu HTML y CSS al cliente lo antes posible.


## "Pero para. Y JavaScript?"

Una aplicación web decente definitivamente va a usar algo de JavaScript. Eso es un hecho.

El "problema" con JavaScript es que podes modificar el contenido y estilo de una página usandolo. Te acordas?

Por ende, podes eliminar y agregar elementos del [DOM](https://developer.mozilla.org/es/docs/DOM) y podrías modificar las propiedades [CSSOM](https://developer.mozilla.org/es/docs/Web/API/CSS_Object_Model) de un elemento a través de JavaScript también.

Esto es genial!

Sin embargo, viene con un costo.

Tomá en cuenta este documento `html`

```html
<!DOCTYPE html>
<html>

<head>
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <title>Medium Article Demo</title>
    <link rel="stylesheet" href="style.css">
</head>

<body>
    <p id="header">How Browser Rendering Works</p>
    <div><img src="https://i.imgur.com/jDq3k3r.jpg"></div>
</body>

</html>
```

Es un documento bastante simple.

La hoja de estilos `style.css` tiene una única declaración:

```css
body {
  background: #8cacea;
}
```

Y el resultado es:

![result](https://i1.wp.com/storage.googleapis.com/blog-images-backup/1*dwe_vIFxXA0zzMHwlvS47w.png?ssl=1)

Una simple imagen y texto es renderizado en la pantalla.

Como vimos anteriormente, el navegador lee bytes del archivo `html` del disco (o red) y lo transforma en caracteres. Estos caracteres son analizados y transformados en tokens.

En cuanto el parser llega a la linea `<link rel="stylesheet" href="style.css">`, un pedido se realiza para traer el archivo CSS, `style.css`.

La construcción del DOM continua, y cuando el archivo `css` regresa con algún contenido, la construcción del CSSOM comienza.

¿Qué sucede con este flujo una vez que introducimos JavaScript?

Bueno, una de las cosas más importantes a recordar es que cuando el navegador encuentra un tag `script`, sin importar cuando, la construcción del DOM se pausa!

El proceso entero de construcción del DOM es detenido hasta que el script finaliza su ejecución.

![halted-dom-warning](https://i1.wp.com/storage.googleapis.com/blog-images-backup/1*7Zku0ogP6C2ua43E4Y5ImA.png?ssl=1)

Esto sucede ya que JavaScript puede alterar tanto el DOM como el CSSOM. Y como el navegador no puede estar seguro sobre qué hará este script particular, toma la precaución de detener toda la construcción del DOM.

¿Cuán malo puede ser esto?

Veamos!

En el documento `html` básico que vimos anteriormente, vamos a introducir un tag `script` con JavaScript básico.

```html
<!DOCTYPE html>
<html>

<head>
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <title>Medium Article Demo</title>
    <link rel="stylesheet" href="style.css">
</head>

<body>

    <p id="header">How Browser Rendering Works</p>
    <div><img src="https://i.imgur.com/jDq3k3r.jpg"></div>

    <script>
        let header = document.getElementById("header");

        console.log("header is: ", header);
    </script>
</body>

</html>
```

Dentro del tag `script` estoy accediendo al DOM para tomar un nodo con `id` `header` y luego imprimirlo en consola.

Esto funciona correctamente, como puede verse en la imagen:

![basic-js](https://i2.wp.com/storage.googleapis.com/blog-images-backup/1*d4uD0EVuVSgdML7_07tNbw.png?ssl=1)

Sin embargo, ¿Notaste que el tag `script` está ubicado al final del tag `body`?

Vamos a moverlo al tag `head` a ver que sucede.

```html
<!DOCTYPE html>
<html>

<head>
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <title>Medium Article Demo</title>
    <link rel="stylesheet" href="style.css">
    <script>
        let header = document.getElementById("header");

        console.log("header is: ", header);
    </script>
</head>

<body>

    <p id="header">How Browser Rendering Works</p>
    <div><img src="https://i.imgur.com/jDq3k3r.jpg"></div>
</body>

</html>
```

Una vez que hago esto, la variable `header` resuelve `null`.

![failed-header-var](https://i2.wp.com/storage.googleapis.com/blog-images-backup/1*9h-RJFkX76TT4JuyRxTyiA.png?ssl=1)

¿Por qué?

Muy simple.

Mientras el parser HTML estaba en el proceso de construir el DOM, encontró un tag `script`. En ese momento, el tag `body` y todo su contenido NO habían sido parseados.

La construcción del DOM es detenida hasta que la ejecución del script está completa:

![halted-dom-construction](https://i2.wp.com/storage.googleapis.com/blog-images-backup/1*MBY_mv3GKMgv4Rb2GjhiKg.png?resize=687%2C487&ssl=1)

Para cuando el `script` intento acceder al nodo del DOM con `id` `header`, este no existía porque el DOM no había finalizado de parsear el documento!

Esto nos lleva a otro punto importante.

El lugar donde están tus scripts importa.

![script-location-matters](https://i1.wp.com/storage.googleapis.com/blog-images-backup/1*mhK63PiEos6yZtRN5kwSBQ.png?ssl=1)

Y eso no es todo.

Si extraes el `script` a un archivo local externo `app.js`, el comportamiento es el mismo. La construcción del DOM es detenida.

```html
<!DOCTYPE html>
<html>

<head>
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <title>Medium Article Demo</title>
    <link rel="stylesheet" href="style.css">
    <script src="app.js"></script>
</head>

<body>

    <p id="header">How Browser Rendering Works</p>
    <div><img src="https://i.imgur.com/jDq3k3r.jpg"></div>
</body>

</html>
```

Y eso no es todo.

¿Y si `app.js` no fuese local, si no que es descargada de internet?

```html
<!DOCTYPE html>
<html>

<head>
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <title>Medium Article Demo</title>
    <link rel="stylesheet" href="style.css">
    <script src="https://some-link-to-app.js"></script>
</head>

<body>

    <p id="header">How Browser Rendering Works</p>
    <div><img src="https://i.imgur.com/jDq3k3r.jpg"></div>
</body>

</html>
```

Si la conexión a internet es lenta y tarda miles de milisegundos en traer `app.js`, la construcción del DOM se detendría por miles de milisegundos también!

Recordá que JavaScript puede también acceder al CCSSOM y hacerle cambios. Por ejemplo, esto es JavaScript válido:

```javascript
document.getElementsByTagName("body")[0].style.backgroundColor = "red";
```

Entonces, ¿Qué pasa cuando el parser encuentra un tag `script` y el CSSOM aún no está listo?

Bueno, la respuesta es simple.

La ejecución de JavaScript se verá detenida hasta que el CSSOM esté listo.

![halted-js-cssom](https://i2.wp.com/storage.googleapis.com/blog-images-backup/1*UeR5LCcuy5OtswIzjnF1iQ.png?ssl=1)

Asi que, aunque la construcción del DOM se detiene hasta que un tag `script` que fue encontrado finaliza, no es lo que sucede con el CSSOM.

Con el CSSOM, la ejecución de JavaScript espera. Sin CSSOM, no hay ejecución de JavaScript.

## El atributo async

Por defecto, cada script es un bloqueador del proceso de construcción del DOM, por lo tanto, su construcción siempre será detenida. 

Aunque, hay una manera de cambiar el comportamiento por defecto.

Si añadís la palabra clave ‘async’ a la etiqueta ‘script’, la construcción del DOM no será detenida. La construcción del DOM continuará, y el script será ejecutado cuando haya terminado de descargarse y esté listo.

Aquí hay un ejemplo:

```html
<!DOCTYPE html>
<html>

<head>
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <title>Medium Article Demo</title>
    <link rel="stylesheet" href="style.css">
    <script src="https://some-link-to-app.js" async></script>
</head>

<body>

    <p id="header">How Browser Rendering Works</p>
    <div><img src="https://i.imgur.com/jDq3k3r.jpg"></div>
</body>

</html>
```

## La ruta crítica de renderizado

Todo este tiempo hemos hablado sobre los pasos tomados entre recibir los bytes de HTML, CSS y JS y transformarlos en píxeles renderizados en la pantalla.

Este proceso completo es llamado la ruta crítica de renderizado.

Optimizar tus sitios web para máximo rendimiento se trata de optimizar la ruta critica de renderizado.

Un sitio bien optimizado deberia pasar por un proceso de renderizado progresivo y no tener el proceso entero frenado.





Esta es la diferencia entre una aplicación web percibida como rápida o lenta.

Una buena estrategia de optimización para nuestra ruta crítica de renderizado habilita al navegador a cargar una página lo más rapido posible priorizando cuáles recursos son cargados en el orden en el que son cargados.


## Conclusión

Habiendo entendido los conceptos basicos de cómo tu navegador renderiza los archivos HTML, CSS y JS, te imploro que te tomes el tiempo de explorar cómo podés tomar ventaja de este conocimiento para optimizar tus páginas para más rendimiento.

Un buen lugar para empezar es la sección de rendimiento(https://developers.google.com/web/fundamentals/performance/why-performance-matters/)de la documentación de Google Web Fundamentals.
