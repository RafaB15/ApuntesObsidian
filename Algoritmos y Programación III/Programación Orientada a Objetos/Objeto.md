- Entidad con comportamiento.
- Está definido por: 
	- **Identidad**: Lo que lo distingue de otros objetos de las mismas características. 
	- **Estado**: Los valores de sus *atributos*. 
	- **Comportamiento**: Sus reacciones ante mensajes recibidos y sus acciones en forma de mensajes enviados, implementados mediante *métodos* (en C++ se las llama función miembro).
- En la [[Programación Orientada a Objetos]] son una instancia de una [[Clase|clase]].
- Todo objeto tiene un comportamiento que está dado por las funciones (métodos) que ejecuta cuando recibe solicitudes (mensajes), generalmente de otros objetos. 
- Durante la instanciación de los objetos se ejecutan instrucciones, por ejemplo, para inicializar sus atributos. Este comportamiento está codificado en constructores, los cuales no tienen valor de retorno (ni siquiera void) y deben tener el mismo nombre que su clase. 
- Cada método debe limitarse a realizar una única tarea bien definida, y su nombre debe expresar esa tarea con efectividad. Esto hace que los programas sean más fáciles de escribir, depurar, mantener y modificar.
- Desde el resto de los objetos se debería poder solicitarle a un objeto la ejecución de sus métodos, por eso a estos casi siempre se los califica como public, a menos que solo se invoquen desde dentro del propio objeto, en cuyo caso se los debe hacer invisibles para los demás objetos, calificándolos como private.
- Hay tres formas de invocar un método:
	1. Pasándole un mensaje a un objeto, es decir, usando una variable que se refiera al objeto, seguida de punto (.) y el nombre del método. Por ejemplo: estudiante.listar();
	2. Utilizando el nombre de la clase, seguido de punto (.) y el nombre de un método de la clase. Por ejemplo: Math.sqrt(81.0);
	3. Usando solo el nombre del método, si este es parte de la misma clase. Por ejemplo: cerrar();
- Los métodos pueden devolver como máximo un valor, pero el valor devuelto puede ser una referencia a un objeto que contenga varios valores. El tipo del valor devuelto se indica antes del nombre del método, al declararse este último. 
- Los métodos (pero no los constructores) pueden ser recursivos. 
- La firma (signature) de un método o constructor está compuesta por su nombre y los tipos de sus parámetros, por lo tanto es posible que haya múltiples versiones de un método o constructor, siempre y cuando sus firmas difieran. Esto se denomina **sobrecarga**.
- Una característica importante de las invocaciones de los métodos es la promoción de argumentos. Por ejemplo, se puede llamar al método estático sqrt de la clase Math con un argumento entero, a pesar de que el método espera recibir un double.
- En Java, el pasaje de argumentos a los métodos es por valor si son tipos primitivos, y por referencia en caso de no serlo (ser objetos).
- Si un método o atributo se clasifica como **static**, entonces le pertenece a la [[Clase]] y no a una instancia, por lo que si tenemos la clase Animal, haríamos Animal.método(). Recordar que pueden haber problemas definiendo métodos en una clase main porque al llamarlos no hay una instancia de main.
- Hay public, protected, private y package private (default).
- ![[Pasted image 20240130223158.png]]
- Diagrama en el que vemos que con herencia podemos usar polimorfismo y reutilizamos código. Con una clase abstracta también. Con una interface podemos usar polimorfismo pero no reutilizamos código. Con composición (tener un atributo con un objeto) podemos reutilizar código. Como con los últimos dos podemos lograr polimorfismo y reutilización hay muchos lenguajes modernos como Rust o Go que no implementan herencia, además de que los dos últimos métodos son más fáciles de mantener, en especial cuando en Rust las interfaces SÍ pueden tener implementaciones.
- Si un atributo de un objeto que tiene un objeto dice final, lo que es final es la dirección de memoria. El objeto que es apuntado puede cambiar sus parámetros.
- En intellij hay una solapa problems a la izquierda donde podemos ver todos los errores y advertencias.