### Introducción

# **API DOM**  
  
El código JavaScript puede acceder al contenido de una página utilizando un API denominada DOM (Document Object Model).  
  
El API DOM ha sido estandarizada por el consorcio W3C.  
DOM ofrece dos modos de acceso al contenido de una página:  
- A través del objeto document (DOM nivel 0)  
- Mediante un árbol de objetos/nodos (DOM nivel 1)

# **document**  
  
document representa la página HTML  
  
- Permite el acceso a toda la información del documento.  
  
- Arrays generales (DOM 0):  
  
- Arrays globales para las etiquetas más importantes: forms, links, images, etc.  
  
- Accesibles por índice o por el valor del atributo name.document.forms[“formulario”].submit();  
  
Sin embargo, no se puede acceder a los bloques div ni a otras declaraciones de este modo.

# **Referencias a nodos del documento**  
  
Obtener referencias a declaraciones por el atributo id.  
  
```js 
let logo = document.getElementById(“logo”);
```
Obtener todos los objetos de un tipo de etiqueta (ej.: div)  
```js  
let array = document.getElementsByTagName(“div”);
```
También se puede aplicar sobre cualquier nodo del árbol DOM (ej.: obtener referencias a declaraciones por el atributo name).  
```js  
let logo = document.getElementByName(“un_boton”);`
```

# Tipos de nodos

**Hay dos tipos de nodos:**  
  
![DOM](https://lh3.googleusercontent.com/AFn27IjwRzCt74OYOxm3YJYofOEjls4WRQ6nUF53Db5IgunCP7qDVTnK3kmmV0IbkfkM5_sE85C9z04jzVn20OxOHmrlMV1kLpPMsjWH6OEmaPYzGZNJsSz6UhA-mLEUED4fk7zIWw=w2400)  
  
Los nodos en azul, que corresponden a elementos HTML como `<body>` o  `<p>`. Cada uno de estos nodos puede tener un número infinito de nodos hijos, pero sólo puede tener un nodo padre. La única excepción es el nodo raíz del árbol (html) que no tiene ningún padre.  
  
Los nodos en rojo, que corresponden al contenido textual de la página, no pueden tener nodos hijos.  
  
El navegador web permite visualizar los elementos de una página web a través de la consola para desarrolladores. Sólo hay que abrir la consola y en la pestaña llamada Elementos se encuentra la estructura de la página. Es posible navegar por la estructura desplegando los diferentes nodos correspondientes a las etiquetas HTML.

# **Acceder al DOM con el objeto document**  
  
Cuando un programa JavaScript, se ejecuta en el contexto de un navegador, se puede acceder al DOM utilizando el objeto "document", corresponde al elemento `<html>`, con lo que se tendrá acceso a todos los nodos hijos de la página, como `<head>` o `<body>` y sus descendientes.  
  
Ejemplo:   
  
JS
```js
let h = document.head; // La variable h contiene el objeto head del DOM
console.log(h);   
let b = document.body; // La variable b contiene el objeto body del DOM   
console.log(b);
  ```
Código HTML  
```html
<script src="../js/ejJs1.js"> </body>   </html>
```

# **Obtener el tipo de un nodo**  
  
Cada objeto del DOM tiene una propiedad  **nodeType**que indica su tipo. El valor numérico que devuelve esta propiedad, indica el tipo de nodo. El valor es igual a  **document.ELEMENT_NODE** para un nodo "elemento" (etiqueta HTML) y **document.TEXT_NODE** para un nodo de texto document.  
  
Sintaxis  
```js 
let  type =  node.nodeType;
```

donde la variable **type** será un entero positivo con alguno de los siguientes valores (* indica descatalogado):  

ELEMENT_NODE = 1

ATTRIBUTE_NODE = 2

TEXT_NODE = 3

CDATA_SECTION_NODE = 4

ENTITY_REFERENCE_NODE = 5

ENTITY_NODE = 6

PROCESSING_INSTRUCTION_NODE = 7

COMMENT_NODE = 8

DOCUMENT_NODE = 9

DOCUMENT_TYPE_NODE = 10

DOCUMENT_FRAGMENT_NODE = 11

NOTATION_NODE = 12

DOCUMENT_POSITION_DISCONNECTED = 1

DOCUMENT_POSITION_PRECEDING = 2

DOCUMENT_POSITION_FOLLOWING = 4

DOCUMENT_POSITION_CONTAINS = 8

DOCUMENT_POSITION_CONTAINED_BY = 16

DOCUMENT_POSITION_IMPLEMENTATION_SPECIFIC = 32 

Ejemplo:  
```js  
let node = document.documentElement.firstChild;   
if (node.nodeType != Node.COMMENT_NODE)   
console.log("Aquí debería ir un comentario");
```
  
Verifica si el primer nodo dentro de un elemento tipo documento es un comentario nodo, y si no lo es, muestra un mensaje.

# **Acceso a los descendientes de un nodo**  
  
Cada objeto del DOM correspondiente a una etiqueta HTML posee una propiedad **childNodes**. Esta propiedad guarda la lista de todos los nodos hijos bajo la forma de objetos del DOM. Se puedes utilizar esta lista como un **array** para acceder a los diferentes hijos del nodo.  
  
La propiedad **chilNode** no retorna un verdadero array de JavaScript, pero contiene la propiedad **length** para conocer el número de elementos de la lista, o se puede por ejemplo, utilizar el índice para acceder a los diferentes elementos con un bucle.  
  
Ejemplo, recorrer la lista de nodos hijos:  
```js  
let nodes = document.body.childNodes;   
for (var i = 0; i < nodes.length; i++){   
	console.log(nodes[i]);   
}
```

# **Acceso al padre de un nodo**  
  
Cada objeto del DOM posee una propiedad llamada **parentNode** que retorna el nodo padre como un objeto del DOM.  
  
Para el nodo raíz del DOM (el objeto documento), el valor de  **parentNode** es null : document no tiene ningún padre.  
  
Ejemplo, obtiene el nombre del nodo padre de un elemento `li`:  
```html  
<!DOCTYPE html>   
<html>   
	<body>   
	<p>Lista de ejemplo:</p>   
	<ul>
		<li id="myLI">Café</li>   
		<li>Chocolate</li>   
	</ul>   
	<p>Pulsa en el botón para obtener el nombre del nodo padre del elemento li en la lista.</p>   
	<button onclick="myFunction()">Try it</button>   
	<p id="demo"></p>   
<script>   
	function myFunction() {   
		let x = document.getElementById("myLI").parentNode.nodeName;   
	    document.getElementById("demo").innerHTML = x;
	}
</script>
	</body>
</html>
```

# **Introducción a BOM**  
  
Las versiones 3.0 de los navegadores Internet Explorer y Netscape Navigator introdujeron el concepto de _Browser Object Model_ o BOM, que permite acceder y modificar las propiedades de las ventanas del propio navegador.  
  
Mediante BOM, es posible redimensionar y mover la ventana del navegador, modificar el texto que se muestra en la barra de estado y realizar muchas otras manipulaciones no relacionadas con el contenido de la página HTML.  
  
El mayor inconveniente de BOM es que, al contrario de lo que sucede con DOM, ninguna entidad se encarga de estandarizarlo o definir unos mínimos de interoperabilidad entre navegadores.  
  
BOM está compuesto por varios objetos relacionados entre sí. El siguiente esquema muestra los objetos de BOM y su relación:  
  
![BOM](https://lh3.googleusercontent.com/C-3LVcyEMODVoMmcekIjoL6gHqDw5eF7qF7JHPk2VGZ1su-_yuknxnJcjZhNGS4T7xFrE5tS4VvEdOfjO5TJHeI1hyROn4vYUf2V2yGjaSXK9QEJt5XDvYe9R1HuyZUa0klRFvNd5A=w2400)


# **Interfaz Node**  
  
Todos los elementos HTML en el DOM heredan de la interfaz **Node**, incluyendo el objeto **document**. Esta interfaz contiene métodos utilizados para realizar operaciones con otros elementos HTML, como agregar, reemplazar, eliminar o verificar si algún elemento está anidado dentro de otro.  
  
#### **appendChild**  
Agrega un nodo al final de la lista de sus nodos hijos.  
  
#### **cloneNode**  
Clona un nodo, con o sin nodos hijos, dependiendo del valor booleano que se le pase como parámetro.  
  
#### **compareDocumentPosition**  
Compara la posición de un nodo con respecto a otro. El valor devuelto por **compareDocumentPosition** es una máscara de bit, el cual puede tener uno o más de los siguientes valores:  
  

Nombre                                                                                Valor

DOCUMENT_POSITION_DISCONNECTED                          1

DOCUMENT_POSITION_PRECEDING                                  2

DOCUMENT_POSITION_FOLLOWING                                 4

DOCUMENT_POSITION_CONTAINS                                     8

DOCUMENT_POSITION_CONTAINED_BY                          16

DOCUMENT_POSITION_IMPLEMENTATION_SPECIFIC   32
  
#### **contains**  
Devuelve un valor booleano de si un nodo está contenido dentro de otro.  
  
#### **hasChildNodes**  
Verifica si un nodo tiene nodos hijos.  
  
#### **insertBefore**  
Agrega un elemento a la lista de nodos hijos de un nodo, con la diferencia que toma un nodo de referencia para insertarlo antes de él (a diferencia de **appendChild**, que siempre lo agrega al final de la lista).  
  
#### **isEqualNode**  
Verifica si un nodo es igual a otro. Para que sean iguales deben cumplir ciertas condiciones:  
  

- Ambos nodos son del mismo tipo  
- Los siguientes atributos tienen el mismo valor en ambos nodos: nodeName, localName, namespaceURI, prefix, nodeValue.  
- El resto de atributos (accesibles mediante la propiedad attributes) deben ser iguales.  
- Sus nodos hijos deben ser iguales.

  
#### **isSameNode**  
Verifica si tanto un nodo como el otro referencian al mismo objeto en el árbol del DOM. Dos nodos que referencien a un mismo objeto son iguales (**isEqualNode** devolverá true), pero no sucede de forma inversa.  
  
#### **normalize**  
Normaliza un nodo y sus nodos hijos. En una forma normalizada, un nodo no tiene nodos de texto vacíos ni existen dos o más nodos de texto adyacentes.  
  
#### **removeChild**  
Elimina un nodo de la lista de sus nodos hijos. El método devuelve una referencia al nodo eliminado, el cual sigue existiendo en memoria pero ya no es parte del árbol del DOM y que puede ser reutilizado luego.  
  
#### **replaceChild**  
Reemplaza un nodo hijo con otro. El método devuelve una referencia al nodo que ha sido reemplazado, al igual que **removeChild**.  
  
#### **hasAttributes**  
Verifica si un nodo tiene atributos o no.

# **Instancias de node, propiedades**  
  
#### **childNodes**  
Devuelve una lista "viva" instancia de **NodeList** con todos sus nodos hijos.  
  
#### **firstChild**  
Devuelve el primer nodo hijo.  
  
#### **lastChild**  
Devuelve el último nodo hijo.  
  
#### **parentNode**  
Devuelve el nodo padre.  
  
#### **parentElement**  
Similar a **parentNode**, excepto que solo devuelve un nodo si el nodo padre es una instancia de Element. En caso contrario, devuelve null.  
  
#### **nextSibling**  
Devuelve el nodo hermano siguiente. Dos nodos son hermanos cuando están al mismo nivel en un árbol y comparten el mismo nodo padre.  
  
#### **previousSibling**  
Devuelve el nodo hermano anterior.  
  
#### **nodeName**  
Devuelve el nombre de la etiqueta.  
  
#### **localName**  
En HTML, el valor de **localName** es similar a **nodeName** pero en minúsculas.  
  
#### **nodeValue**  
Si el nodo es texto, comentario o atributo, devuelven sus correspondientes valores. Para elementos, o para **document**, devuelve null.  
  
#### **nodeType**  
Devuelve un número, correspondiente al tipo de nodo.  
  
#### **textContent**  
Devuelve una cadena con el contenido de un nodo, resultado de unir todos los valores de **textContent**de sus nodos hijos. Si un nodo solo tiene un nodo de texto como nodo hijo, el valor de **textContent** es una cadena con el contenido del texto.

# **Interfaz Element**  
  
Todos los elementos HTML en el DOM heredan de la interfaz **Element**, la misma que hereda de la interfaz **Node**. Esta interfaz contiene métodos utilizados para realizar operaciones dentro de un elemento, como manipular atributos u obtener elementos anidados según criterios como clase o selector CSS, o nombre de etiqueta.  
  
#### m**getAttribute**  
Devuelve una cadena con el valor de un atributo definido como parámetro.  
  
#### **setAttribute**  
Define o reemplaza un atributo, con su respectivo valor.  
  
#### **removeAttribute**  
Elimina un atributo definido como parámetro.  
  
#### **hasAttribute**  
Verifica si un atributo está definido en un elemento.  
  
#### **getAttributeNode**  
Similar a **getAttribute**, excepto que en vez de devolver una cadena devuelve una instancia de Attr.  
  
#### **setAttributeNode**  
Similar a **setAttribute**, excepto que en vez de asignar un nombre y valor, se debe asignar una instancia de Attr.  
  
#### **removeAttributeNode**  
Similar a **removeAttribute**, excepto que debe pasarse como parámetro una instancia de Attr.  
  
#### **getElementsByTagName**  
Devuelve una instancia de **NodeList** con todos los nodos hijos cuyo nombre de etiqueta sea el pasado como parámetro.  
  
#### **scrollIntoView**  
Desplaza la vista del navegador hasta el elemento que llama a este método. Acepta un parámetro, el cual si es true, alinea el elemento a la parte superior de la vista del navegador, mientras que si es false, lo alinea a su parte inferior.  
  
#### **getElementsByClassName**  
Devuelve una instancia de **NodeList** con todos los nodos hijos que tengan todas las clases pasadas como parámetro. Estas clases deben estar en una cadena y separadas por un espacio.  
  
#### **insertAdjacentHTML**  
Convierte una cadena con HTML en un nodo o conjunto de nodos, según el contenido de la cadena, e inserta el resultado en una posición dada con respecto al nodo. El valor de la posición está definida por los siguientes valores:  

- **beforebegin**: Antes del elemento  
- **afterbegin**: Antes del primer nodo hijo del elemento  
- **beforeend**: Después del último nodo hijo del elemento  
- **afterend**: Después del elemento  
  
#### **querySelector**  
Devuelve el primer elemento hijo que concuerde con un selector CSS dado.  
  
#### **querySelectorAll**  
Devuelve una lista instancia de **NodeList** con todos los elementos hijos que concuerden con el selector CSS que se le pase como parámetro. En este caso, el resultado de **querySelectorAll** no es una lista "viva".  
  
#### **matchesSelector**  
Verifica si un elemento concuerda con un selector CSS dado.  
  
Al ser un método relativamente nuevo y en modo experimental, los navegadores le agregan un prefijo según cada implementación: webkitMatchesSelector, mozMatchesSelector, oMatchesSelector o msMatchesSelector.  
  
#### **getClientRects**  
Devuelve una lista instancia de **ClientRectList** con objetos **TextRectangle**, los cuales indican tanto el tamaño del elemento como la posición con respecto al viewport (la zona visible del documento en el navegador). Si el elemento es inline (propiedad display: inline en CSS), **getClientRects** devolverá un objeto **ClientRect** por cada línea de texto dentro del elemento.  
  
#### **getBoundingClientRect**  
Devuelve una instancia de **TextRectangle**(ClientRect en Webkit y DOMRect en Gecko) con el tamaño del elemento y su posición con respecto al viewport.  
  
#### **remove**  
Elimina un elemento del árbol del DOM. Este método no devuelve el elemento eliminado, por lo que se si desea tenerlo guardado en memoria primero se debe guardar una referencia del nodo a eliminar en una variable.

## **Así mismo, tiene las siguientes propiedades:**  
  
#### **attributes**  
Devuelve una instancia de NamedNodeMap con todos los atributos de un elemento.  
  
#### **children**  
Devuelve una lista "viva" instancia de **HTMLCollection** con los nodos hijos del elemento que son elementos.  
  
#### **childElementCount**  
Devuelve el número de nodos hijos que son elementos.  
  
#### **firstElementChild**  
Devuelve el primer nodo hijo que es un elemento.  
  
#### **lastElementChild**  
Devuelve el último nodo hijo que es un elemento.  
  
#### **nextElementSibling**  
Devuelve el siguiente nodo hermano que sea un elemento.  
  
#### **previousElementSibling**  
Devuelve el anterior nodo hermano que sea un elemento.  
  
#### **classList**  
Devuelve una lista instancia de **DOMTokenList** con todas las clases asignadas al elemento.  
  
#### **className**  
Devuelve una cadena con el valor del atributo class.  
  
#### **clientHeight** 
Devuelve el alto de un elemento, incluyendo el padding superior e inferior (definido por la propiedad padding en CSS), pero sin contar el espacio de la barra de desplazamiento (si la hubiera), ni el margen (margin en CSS) o tamaño de borde (border-width en CSS).  
  
#### **clientLeft**  
Devuelve el ancho del borde izquierdo de un elemento, incluyendo el ancho de la barra de desplazamiento vertical, si la hubiera.  
  
#### **clientTop**  
Devuelve el alto del borde superior de un elemento. No incluye ni margen ni padding superiores.  
  
#### **clientWidth**  
Devuelve el ancho de un elemento, incluyendo el padding a la izquierda y derecha, pero sin contar el espacio de la barra de desplazamiento (si la hubiera), bordes o márgenes.  
  
#### **id**  
Devuelve una cadena con el valor del atributo id.  
  
#### **innerHTML**  
Devuelve una cadena con el contenido de un elemento en forma de HTML.  
  
**outerHTML** Similar a innerHTML, pero incluye las etiquetas HTML del elemento.  
  
#### **scrollHeight**  
Devuelve el alto de un elemento, incluyendo su padding superior e inferior, pero no sus márgenes. Si el contenido del elemento sobrepasa un alto definido previamente y aparecen barras de desplazamiento, scrollHeight devolverá el alto del contenido total, incluyendo el que está visible y el que no.  
  
#### **scrollLeft**  
Devuelve la posición del contenido del elemento con respecto al borde izquierdo del elemento.  
  
#### **scrollTop**  
Devuelve la posición del contenido del elemento con respecto al borde superior del elemento.  
  
#### **scrollWidth**  
Devuelve el ancho de un elemento, incluyendo su padding derecho e izquierdo, pero no sus márgenes. Si el contenido del elemento sobrepasa un ancho definido previamente y aparecen barras de desplazamiento, **scrollWidth** devolverá el ancho del contenido total, incluyendo el que está visible y el que no.  
  
#### **tagName**  
Devuelve el nombre de la etiqueta, en mayúsculas. Similar a **nodeName**  


## **Objeto document**  
  
Entre los atributos que tiene un objeto document se encuentran:  
  
#### **documentElement**  
Devuelve un elemento que representa a la etiqueta html.  
  
#### **title**  
Devuelve el contenido de la etiqueta , o uno asignado manualmente.  
  
#### **head**  
Devuelve un elemento que representa a la etiqueta head.  
  
#### **body**  
Devuelve un elemento que representa a la etiqueta body.  
  
#### **styleSheets**  
Devuelve una lista instancia de **StyleSheetList** con objetos **CSSStyleSheet**, uno por cada hoja de estilos definida o enlazada al documento (con ).  
  
#### **cookie**  
Devuelve una cadena con todas las _cookies_asignadas al documento actual.  
  
#### **location**  
Devuelve un objeto **Location**, el cual contiene información sobre la URL actual del documento. Esta propiedad puede ser cambiada, asignando una cadena con la nueva URL a la cual el navegador direccionará.  
  
**document** también tiene algunas propiedades de la interfaz Element, como **children**, **firstElementChild**, **lastElementChild** y **childElementCount**.  
  
Así mismo, tiene métodos que sirven para crear elementos, y acceder a cualquier elemento dentro del documento:  
  
#### **createAttribute**  
Crea un nodo atributo (instancia de Attr) con un nombre pasado como parámetro.  
  
#### **createComment** 
Crea un nodo comentario con el contenido pasado como parámetro.  
  
#### **createElement**  
Crea un nodo elemento con el nombre de la etiqueta pasado como parámetro.  
  
#### **createTextNode**  
Crea un nodo texto con el contenido pasado como parámetro.
