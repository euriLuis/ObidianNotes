# El modelo de objeto del documento.

## Estructura del documento.
> La estructura de datos que el navegador utiliza para representar el documento  sigue esta forma. Para cada caja, hay un objeto con el que podemos interactuar para saber cosas como qué etiqueta HTML representa y qué cajas y texto contiene. Esta representación se llama Modelo de Objetos del Documento, o DOM en resumen.

## Movimientos a través del árbol.

Cada nodo presenta una propiedad

- ` parentNode` que apunta al padre.

- `childNodes` que apunta al hijo.

- `firstChild` y `lastChild` que apunta al primer y último hijo.

- `previousSibling` y `nextSibling` que apuntan a los nodos adyacentes.

*En caso de no poseer nodos con esa propiedad retornaran `null`*
## Encontrando elementos

Todos los nodos de elemento tienen un método `getElementsByTagName` que recoge todos los elementos con el nombre de etiqueta dado que son descendientes (hijos directos o indirectos) de ese nodo y los devuelve como un objeto similar a un array.

```js

let enlace = document.body.getElementsByTagName("a")[0];

console.log(enlace.href);

```

Para encontrar un nodo específico único, puedes darle un atributo id y usar `document.getElementById` en su lugar.

```html

<p>Mi avestruz Gertrudis:</p>

<p><img id="gertrudis" src="img/ostrich.png"></p>

  

<script>

  let ostrich = document.getElementById("gertrudis");

  console.log(ostrich.src);

</script>

```

Un tercer método similar es `getElementsByClassName`, que, al igual que busca a través del contenido de un nodo de elemento y recupera todos los elementos que tienen la cadena dada en su atributo class.

## Cambiando el documento.

Casi todo se puede cambiar en la estructura de datos del DOM.
Los nodos tienen un método `remove` para removerlos de su nodo padre actual.
Para añadir un nodo hijo a un nodo de elemento, podemos usar `appendChild`
`insertBefore`, que inserta el nodo

dado como primer argumento antes del nodo dado como segundo argumento.

  

```html

  <p>Uno</p>

  <p>Dos</p>

  <p>Tres</p>

  <script>

    let párrafos = document.body.getElementsByTagName("p");

     document.body.insertBefore(párrafos[2], párrafos[0]);

</script>

```

  
  
  

## Resumen.

```js

    parentNode //apunta al padre.

    childNodes //apunta a todos los hijos.

    firstChild //apunta al primer hijo

    lastChild //apunta al último hijo

    previousSibling //nodo antecesor

    nextSibling //nodo sucesor

    /*---------------------------*/

    getElementsByTagName //selecciona los elementos hijos de un nodo según la etiqueta.

    getElementById //selecciona el elemento hijo de un nodo según el ID.

    getElementsByClassName //selecciona los elementos hijos de un nodo según la clase.

    /*----------------------------*/

    remove //remueve un nodo

    appendChild //agrega un nodo hijo al final.

    insertBefore //agrega in nodo hijo antes del nodo especificado.

```

