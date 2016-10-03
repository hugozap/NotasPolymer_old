-- Motivación:
Los devs que estén creando soluciones que requieran interacción tipo drag and drop ahorrarán tiempo y podrán construirlas utilizando como punto de partida mi investigación. 

	<interact-drop-zone>

Se puede encapsular la funcionalidad de interact ( dropable ) y draggable
con el fin de facilitar el uso
como behavior : Dropzone

Otro behavior puede ser el draggable que permite que un elemento sea draggable.


-- /Motivación
Drag and drop with Polymer 1.0 and interact.js

Una opción mientras sale la versión oficial es utilizar interact, crear un shim y preparar.

Interact permite crear interacciones drag and drop, Podemos integrarla en nuestros elementos para soportar drag and drop. Basta con importar el elemento wrapper de interact y tendremos acceso al componente.


## Creando el elemento

## Acerca de Iteract.JS

Es una librería creada específicamente para interacciones de tipo drag and drop
tiene una interfaz facil de entender y una documentación clara

TODO: incluir referencia a la documentación aquí.

### Configurando la dependencia a interactjs.

Puedes instalar con bower el paquete wrapper de interactjs como elemento de Polymer

	npm install polyinteractjs

Ahora se debe incluir como dependencia en el elemento (padre) donde deseemos utilizar comportamientos de drag and drop.

	<link rel="import" href="/bower_components/polyinteractjs/interactjs.html">

Con la dependencia correctamente configurada ya tenemos acceso a la funcionalidad de drag drop que nos ofrece la librería.

TODO: link a docs interact aquí.

En nuestro ejemplo vamos a simular un board de cartas, donde se pueda arrastrar una carta a unos sitios previoamente seleccionados.

TODO: link a ejemplo funcionando aquí.
TODO: link a ejemplo en github aquí.

En el ejemplo tenemos dos componentes Board y Card,
lo que queremos es arrastrar nuestra carta a los espacios.

[Svg creado por Lloyd Humphreys](https://thenounproject.com/Lloyd/)
 
## Arrastrando elementos del Shadow DOM

