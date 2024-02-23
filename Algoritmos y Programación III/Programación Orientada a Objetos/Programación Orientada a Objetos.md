> En vez de un procesador de bits consumiendo estructuras de datos, tenemos un universo de **objetos** bien comportados, cada uno de ellos pidiéndole a otro que cortésmente le realice sus variados deseos.

- Se trabaja con **[[Objeto|objetos]]** que actúan para resolver un problema, respondiendo a estímulos (mensajes o eventos) del medio externo. 
- En sistemas diseñados como un conjunto de servicios, por lo general se tendrá un disparador y luego un objeto irá llamando a otro hasta que todo el sistema se pone en movimiento.

# Diseño

## Encontrar Objetos

- Entidades del dominio del problema.
- Se comienza con el diseño de un **[[Modelo|modelo]]**, usando la [[Algoritmos y Programación III/Programación Orientada a Objetos/Abstracción|abstracción]] para representar lo que necesitamos de los objetos físicos para nuestros fines.
## Determinar Mensajes

- Cómo deben interactuar los [[Objeto|objetos]].
- [[Diagramas de Secuencia]] 

## Implementar el comportamiento de los objetos

- La mayor parte de los lenguajes agrupan los objetos en [[Clase|clases]] y es en la definición de estas en donde se definirá el comportamiento de los objetos.

# Principios

## Tell, don't ask!

- Es una buena práctica de evitar solicitarle a un objeto que indique su estado y luego llevar a cabo una acción basándose en este, en lugar de solicitarle al objeto que lleve a cabo la acción él mismo.
- Si tenemos los datos por un lado y la lógica por otro, es programación imperativa tradicional y no lo deberíamos hacer en este paradigma.

## Less is more

- Es una buena práctica de dividir grandes [[Diagramas de Secuencia]] en varios diagramas de menor tamaño y mejor enfocados en lo que se quiere comunicar.
- [[Diagramas de Secuencia#Reglas|Reglas]]
