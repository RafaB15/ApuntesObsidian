# Repaso Job Vacancy

## Controllers 

Puntos de entrada a la aplicación (simil app.rb en alarma)
Están definidios los endpoints para cuando estamos navegando y queremos acceder a un endpoint.

## Views

Frontend -> Simil html con código ruby (files.erb)

## Repositories

Acceso a persistencia de datos
Una cosa son los objetos que yo tengo y otra es como los guardo en bases de datos.
La capa repositories se encarga de como guardar nuestros objetos y guardarlos en los lugares indicados. 
## Model

Lógica de negocio (Cuándo una oferta es vieja)



# Job Vacancy

- Como nos hablaron de números, entonces la experiencia se tendría que representar y guardar en la bdd como número.
- El if para mostrar el not specified se hace en la capa de View por ser una cuestión de presentación.
- Los helpers son para poder poner lógica en las vistas sin tirarlas en el html, era otra forma de hacer lo del not specified.
- MVC vs Hexagonal: La arquitectura de este proyecto es MVC, model view controller.  La hexagonal habla más del concepto de la separación de capas y sus responsabilidades. MVC o clean arquitecture, o hacés una o hacés otra, pero en ambas puede estar una arquitectura hexagonal.
- La estructura de archivos nos la da también el framework.

# Gherkin + Cucumber

- Gherkin -> Lenguaje
	- Lenguaje para escribir pruebas de aceptación en un lenguaje común, no técnico.
- Cucumber -> Framework de ejecución
	- Agarra un gherkin y ejecuta los tests

## Gherkin - Checklist

- **Concreto:** Los ejemplos deben usar datos concretos y reales.
- **Esencial**: Todo datos tuilizado en lso ejemplos debe contribuir al entendimiento del comportamiento que se pretende ilustrar.
- **Enfocado**: cada ejemplo debe enfocarse en 1 interacción.
- **Interesante:** Cada ejemplo debe tener una razón de ser. Cada uno debe tener un nombre que releve su intención.
- **Declarativo:** Los ejemplos que declaran lo que el usuario está intentando hacer son más fáciles de entender y mantener que aquellos que describen imperativamente lo que el usuario hace (no decir que presiona un botón azul, sino qué implica).
- **Obicuos:** Hay que evitar términos que solo sean entendidos por algunos miembros del equipo. Es mejor evitar lenguaje técnico y usar terminología de negocio.


## Consejos

- Una regla por escenario.
- Puede resultar práctico su escritura en orden inverso: Entonces, Cuando, Dado.
- Solo un "Cuando" por escenario.
- Enfocarse en el "Que". no en el "Como", evitar elementos visuales.
- Máximo 5 pasos por escenario.
- Nada de emociones (Quiero...)
- Omitir pasos obvios (la aplicación está funcionando)

- Necesitamos gherkin y cucumber
![[Pasted image 20240404090845.png]]

Agregamos la gema y hacemos el bundle install


bundle exec cucumber --init nos va a crear las carpetas que el propio framework entiende.

New file departamento alarma.features, 
![[Pasted image 20240404091006.png]]

![[Pasted image 20240404091217.png]]

![[Pasted image 20240404091600.png]]

![[Pasted image 20240404091641.png]]

![[Pasted image 20240404091735.png]]

Poner comillas acostadas si tenemos #{variables}. String estático simples, comillas dobles soportan interpolación con variables. Comillas acostadas querés que EJECUTEN lo que está adentro y te devuelva el resultado

Las reglas de negocio tienen que estar en nuestros modelos. Las validaciones siempre deben estar en los modelos de negocio.

La única forma en la que cambie el gherkin es si me pide un cambio el usuario.
Podemos tocarlos para tener variables.

Es necesaria cierta uniformidad en cómo se escriben los escenarios. De esa forma se va a permitir la re utilización de steps.

Primero escribimos todos los gherkins en wip. Luego empezamos a hacer test unitarios

Primero modelo o steps? Los steps interactúan con la aplicación como una caja negra. El tema con el job vacancy: Hay 3 tipos de steps y la prueba es el WHEN. El THEN es un assert y el given es settear el contexto. El when intentaremos hacerlo como lo hace el usuario. En el then hacemos la verificación o contra la pantalla o incluso contra la bdd.