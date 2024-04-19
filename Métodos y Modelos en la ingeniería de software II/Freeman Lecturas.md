# TDD

![[The fundamental TDD cicle.png]]

![[Inner and Outer feedback loops in TDD.png]]

- Tipos de tests:
	- **Acceptance**: Does the whole system work? 
	- **Integration**: Does our code work against code we can't change? 
	- **Unit**: Do our objects do the right thing, are they convenient to work with?
- **External Quality** is how well the system meets the needs of its customers and users (is it functional, reliable, available, responsive, etc.)
- **Internal Quality** is how well it meets the needs of its developers and administrators (is it easy to understand, easy to change, etc.)

![[Internal vs External Quality.png]]

- We only write code when there is a failing test.
# Walking Skeleton

A “walking skeleton” is an implementation of the thinnest possible slice of real functionality that we can automatically build, deploy, and test end-to-end.
It should include just enough of the automation, the major components, and communication mechanisms to allow us to start working on the first feature.

En nuestro walking skeleton tenemos que también testear deployment, pues es lo que suele fallar cerca de la entrega si no lo testeamos.

# Maintaining the Test-Driven Cycle

- Empezamos cada feature con un acceptance test.
	- La escribimos utilizando únicamente terminología del dominio de la aplicación.
	- Luego tendremos que escribir unit tests para crear la funcionalidad de los objetos hasta que los acceptance tests pasen.
- Los tests de aceptación para features completadas encuentras regresiones y siempre deberían pasar.
- Los tests de aceptación nuevos representan trabajo en progreso y no pasarán hasta que una feature esté lista.
- Si los requerimientos cambian, movemos los test de aceptación afectados fuera de la pila de regresión, y de vuelta a la pila de in progress, los cambiamos para reflejar los nuevos requerimientos y cambiamos el sistema para que pasen de nuevo.
- Empezamos probando el caso de éxito más simple.
- Cuando nuestros tests fallen tenemos que ver que sea por la razón que nosotros esperábamos. Si es una razón distinta, hay que manejar ese caso también.

![[Diagnóstico TDD.png]]

- Usamos los unit tests para testear comportamiento, no métodos.
- Si tenemos dificultades para testear una parte de nuestro código, eso nos puede indicar que hay que mejorar el diseño.

# Estilo orientado a objetos

- **Separation of concerns:** Que cada objeto se encargue de algo específico y si queremos cambiarlo el código esté en un solo lugar.
- **Mayores niveles de abstracción:** Se evita la complejidad trabajando con grandes niveles de abstracción.

![[Modelo de dominio central de una aplicación.png]]

- **Encapsulación:** Se asegura de que el comportamiento de un objeto solo pueda ser afectada a través de su API.
- **Ocultar información:** Esconde cómo un objeto implementa su funcionalidad detrás de la abstracción de su API.
- **Single Responsibility Principle:** Cada objeto deberá tener una única y precisa responsabilidad.
- La API de un objeto compuesto por otros objetos no puede ser más complicada que la suma de sus partes.