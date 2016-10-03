Comunicación entre elementos de la página.

En una página podemos tener múltiples elementos , cada uno con responsabilidades distintas. Es común que queramos tener un mecanismo para que ellos se puedan comunicar. Tenemos varias opciones.

* Por medio de eventos disparados por un elemento y capturados por aquellos elementos interesados.
* Por medio del Api de cada elemento (llamando sus métodos)
* Por medio de un bus de eventos

## Disparando y subscribiendose a eventos generados por otro componente.

Si tenemos dos componentes A y B, y sabemos que cada ciertos segundos B genera un evento con datos que nos interesan, entonces podemos subscribir a A para que realice alguna operación cada vez que B genere el evento.

### Disparar un evento

	this.fire(options...)

Los componentes que requieran disparar eventos deben usar el método fire para ello. Tienen la oportunidad de pasar datos asociados, así como opciones como "bubbling" que indica si el evento opdrá ser capturado por elementos padres ( en la jerarquía DOM ) del elemento que emite el evento.

Disparar un evento es simple, ejemplo:
	
	this.fire('dataAvailable', {someData:someValue} )

Si se quiere especificar opciones adicionales del evento podemos pasar un tercer argumento con la siguiente información.

	AQUI OPCIONES ADICIONALES

## Usando un bus de eventos.

En un bus de eventos, los componentes no saben quienes emiten ni quienes reciben los eventos. Existe un elemento llamado bus de eventos que ofrece las facilidades de disparar un evento y subscribirse a un evento.

[[Architecture note]]

Hay que tener precaución cuando se usan buses de eventos, pues aunque en ciertos casos permiten crear soluciones desacopladas, tienen la desventaja de que el flujo de los datos se hace menos claro. Si tenemos múltiples componentes disparando el mismo evento y otros tantos monitoreando, puede dificultarse hacer seguimiento al flujo de los datos dentro de la aplicación. Puede ser mejor en estos casos que un elemento "padre" sirva como mediador de elementos hijos y sea el quien decida que métodos del Api llamar.