# Styling


## Shared Styles

A partir de la versión 1.1 se pueden incluir referencias a estilos compartidos para ello necesitamos
1 archivo donde los estilos se encuentran encapsulados en un dom-module

	<dom-module id="my-shared-styles">
		<template>
			<style>

			/* CSS rules added here could be used by modules that include this module */
				
			</style>
			
		</template>
	</dom-module>

[[Note]]
Fíjese que estamos guardando nuestros estilos de la misma manera que creamos un componente, como archivo .html, y no como css separado. ( Las versiones anteriores de Polymer recomendaban tener el CSS separado, pero esto cambió y ahora se prefiere tenerlos como módulos dom-module)

[[Note]]
Es importante que el módulo tenga atributo id, para que pueda ser después incluido desde los componentes.

2 Agregar referencia en cada uno de nuestros componentes

	<link rel="import" href="my-shared-styles.html"> 

3 Especificar que queremos incluir los estilos. Agregar la siguiente instrucción dentro del elemento template del elemento desde el cual queremos usar los estilos.

	<template>
		...
	<style include="my-shared-styles"></style>

	</template>

## Note on binding class

Use multiple class names
