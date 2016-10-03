## Data Binding System in Polymer.

El sistema de data binding permite que los datos y los controles estén sincronizados. Cuando el usuario interactúa con un control (e.g input ) estos cambios son reflejados en el modelo que se encuentra asociado.

### Conceptos básicos del databinding.

* Modelo ( objeto que contiene los datos )
* UI ( Controles que pueden mostrar/editar )


Como se realiza la sincronización

En este caso el usuario interactúa con un control (input/select) y esta interacción debe resultar en la actualización del modelo asociado.

Usuario -> Control
Control -> Data Binding
Data Binding -> Modelo

Hasta ahora el proceso de data binding es de una sola vía, es decir que solo estamos preocupados acerca de actualizar una de las dos partes ( el modelo ) cuando la otra parte cambia ( el control UI ).

Cuando hablamos de Data Binding de dos vías ( Two Way Data Binding ) hacemos referencia a que se soportan los dos escenarios:

1) Actualizar el modelo cuando cambia el control de UI
2) Actualizar el control UI cuando el modelo cambia 

[[NOTE]]
En Polymer cuando hablamos de data binding, de dos vías podemos referirnos a la conexión entre dos componentes. No únicamente entre un control de UI y el modelo de datos.

En nuestro ejemplo, queremos mostrar los detalles de una canción. En este caso solo necesitamos mostrar y no editar los datos razón por la cual podemos usar data binding de una sola vía.

Detalles de Canción -> Control UI que muestra los detalles de la canción.

Podemos pasarle el objecto de js contenedor de los detalles de la canción, o podemos también usar como atributos las propiedades de cada canción.

Opción 1: Suponiendo que en nuestro componente padre tenemos una propiedad llamada currentSongDetails que contiene el objeto con las propiedades de la canción que requerimos

	<song-details-panel song="[[currentSongDetails]]"> </song-details-panel>

Opción 2: Pasando como atributo cada una de las propiedades particulars del objeto

	<song-details-panel song-name="[[currentSongDetails.name]]"
	song-duration="[[currentSongDetails.duration]]"
	artist-name="[[currentSongDetails.artistName]]"
	lyrics="[[currentSongDetails.lyrics]]"> </song-details-panel>

[[NOTE]]
La alternativa de pasarle los atributos por separado parece agrandar la declaración. Sin embargo tiene una gran ventaja y es que el componente song-details-panel no necesita conocer la estructura del objeto ( como en el caso 1). Y puede hacer más facil compartir este componente con otros desarrolladores.
[[/NOTE]]

[[NOTE]]
Be careful with setters.

Do not override setters , because Polymer use them for all the declared properties.
[[/NOTE]]

Resource: https://www.youtube.com/watch?v=1sx6YNn58OQ


### Polymer and Knockout

Esta sección puede ser útil para quien tenga experiencia previa con Knockout. Una librería solida que ha pasado la prueba del tiempo y ha demostrado ser robusta / simple y con excelente documentación.

Soy fan de Knockout, especialmente porque es una librería que no intenta hacerlo todo. Sino que se especializa en data binding y lo hace muy bien. Las características atractivas son aquellas que toda librería/componente debe aspirar:

* Es pequeña. No tiene una gran cantidad de conceptos por aprender
* No es un framework: No intenta imponer una forma de construir y crear la arquitectura de la aplicación. 
* Documentación clara: El sitio es claro y es fácil encontrar la referencia a un binding, al igual que ejemplos que le permitan a uno continuar.

Nota:

Así como en knockout se usa ko.dataFor , en polymer se puede utilizar itemForElement para obtener el item del modelo que está asociado con el elemento de la plantilla.

Ej. Mostrar una lista y al hacer click, obtener el elemento del modelo a partir del DOM.
Esto también es util si se quiere hacer algun ajuste al elemento tan pronto el template modifica el DOM con el contenido de los elementos según el databinding.

Por ejemplo, si se quisiera modificar la posición de un elemento con base en los datos, pero si necesidad de crear un elemento aparte, sino accediendo al DOM y realizando el cambio directamente ahí


[[NOTE]]
Aunque Knockout tiene un mecanismo que permite crear componentes, en esta sección nos enfocamos en características de DataBinding.
[[/NOTE]]

#### Ej. Lista de canciones.

Supongamos que queremos crear una aplicación Web que muestre un listado de canciones que se cargan de un servidor usando interfaces REST. Vamos a enfocarnos en el data binding para las dos soluciones ko y polymer para poder resaltar algunas diferencias importantes.

#### Computed methods / Computed observables.

Los Computed Methods sirven para mostrar datos que se "calculan" a partir de nuestro modelo de datos, pero que no los tenemos explícitamente.  El típico ejemplo es concatenar el nombre y apellido de un usuario. En este caso quisiéramos mostrar un link de búsqueda en youtube con el nombre del artista.

E.j : https://www.youtube.com/results?search_query=[ARTIST NAME HERE]

En Polymer ( Componente: SongHeaderDetails ):

	properties:{

		"artistName":{
			type:String
		},
		"youtubequery":{
			type:String,
			computed:"_getYoutubeQueryLink(artistName)"
		}
	}

#### [GOTCHA] Los datos de mi modelo cambiaron pero los cambios no se ven reflejados en la UI, notifyPath y set

Algunos componentes pueden tener un comportamiento que hace que los datos cambien periódicamente. Por ejemplo un componente que carga los datos en un intervalo de 5 segundos.

Si tenemos configurado nuestro binding entonces porqué razón no se actualizan los datos cuando estos cambian?

TODO: Ejemplo Aquí.

La razón es que por cuestiones de Performance, Polymer no monitorea los cambios en el modelo que está asociando (bind) a los controles de interfaz. Es responsabilidad nuestra notificar que hemos cambiado dicho modelo.

Como notificamos de cambios en nuestro modelo a Polymer para que actualice el DOM?

	... Código que cambia o recibe los nuevos datos ...
	
	this.set('propertyName', nuevoValor);

Cuando utilizamos 'set' estamos asignando el valor y notificando al mismo tiempo
También tenemos la opción de utilizar

	this.myProperty = 
	this.notifyPath('myProperty', this.myProperty)

Nota: notifyPath NO cambia nuestro modelo. Primero debemos asignar el valor a la propiedad.

[GOTCHA] Uso de templates 'dom-if' y modificación de elementos

## Acceder a los elementos de un dom-repeat.
(Validar esto). Si se intenta acceder directamente a uno de los elementos, estos no estarán listos, pues es probable que el dom-repeat aún no haya realizado las modificaciones del DOM. 

E.g
	Polyer.dom(this.root).querySelectorAll(".SelectorElemInsideDomRepeat")

Esto retorna un array vacío, entonces como hacemos para solucionarlo?
La solución es suscribirse al evento dom-change de la plantilla que nos indica que ya se hicieron los cambios al dom y se han insertado los elementos.

