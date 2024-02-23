- En el diseño orientado a objetos, reconocer la semejanza entre las cosas nos permite exponer los puntos en común dentro de abstracciones. 
- La identificación de [[Clase|clases]] y [[Objeto|objetos]] implica tanto el descubrimiento como la invención. 
	- A través del descubrimiento, llegamos a reconocer las abstracciones que forman el vocabulario del dominio del problema. 
	- A través de la invención, ideamos abstracciones generalizadas.
- La **herencia** es una forma de reutilización de software en la que se crea una nueva clase aprovechando los miembros de una clase existente o de varias.
- A la clase previamente existente se la conoce como **superclase** (o clase base), y a las nuevas como **subclases** (o clases derivadas). 
- Cada subclase se puede convertir en la superclase de futuras subclases.
- Los atributos y métodos privados no se pueden ni heredar ni usar desde otra clase. 

# Jerarquía de clases

- Una subclase generalmente agrega sus propios atributos y métodos. Por lo tanto, una subclase es más específica que su superclase y representa a un grupo más especializado de [[Objeto|objetos]].
- Generalmente, la subclase exhibe los comportamientos de su superclase junto con otros adicionales específicos de esta subclase. Es por ello que a la herencia se la conoce a veces como **especialización** (superclase -> subclase) o **generalización** (subclase -> superclase): la flecha se lee es un(a).
![[Jerarquía de herencias.png]]

- La **superclase directa** es la clase de la cual la subclase hereda en forma explícita.
- Una **superclase indirecta** es cualquier clase que se encuentre arriba de la superclase directa en la jerarquía de clases, que es la jerarquía que define las relaciones de herencia entre las clases.

# Clase Object

En [[Java]], la jerarquía de clases tiene la clase Object (en el paquete java.lang) en su cima. De ella heredan todas las clases en Java, ya sea en forma directa o indirecta. Por ejemplo, todas heredan de Object el método ``toString`` que es invocado, por ejemplo, al imprimir el objeto.

# Redefinición de métodos

- En caso de que un método de la superclase no sea apropiado para una subclase, ya que en esta se requiere una versión personalizada del método, esta puede **sobrescribir** el método de la superclase con una implementación apropiada.

# Constructores

- Los constructores no se heredan.
- En Java, todas las clases tienen un constructor por defecto: el constructor sin parámetros.
- Igual que con todos los constructores, su primera tarea es llamar al constructor de su superclase directa, para asegurar que las variables de instancia heredadas de la superclase se inicialicen.
- Esto es así, porque siempre que se crea un objeto de una subclase se empieza una **cadena de llamadas a los constructores**, donde el constructor de la subclase, antes de realizar sus propias tareas, invoca al constructor de la superclase, ya sea en forma explícita (por medio de super) o implícita (llamando al constructor por defecto de la superclase).
- Si se declara un constructor con parámetros, el constructor por defecto deja de estar disponible y, para poder instanciar objetos sin pasar argumentos, es necesario declarar un nuevo constructor sin parámetros.
- Si queremos usar un constructor específico de la superclase, escribimos `super(parámetros)` en el constructor de nuestra clase y se va a construir con el constructor que coincida con esos parámetros.

# Super

Cuando un método de una subclase sobrescribe un método de una superclase, se puede acceder al método de la superclase desde la subclase, si se antepone al nombre del método la palabra clave super y un separador punto (.)

# Clases abstractas

- A veces, todo o parte del comportamiento de ciertos objetos es demasiado específico como para implementarlo en una superclase.
- En tales casos, el método se debe declarar anteponiéndole la palabra reservada abstract en la superclase e implementarse en cada subclase.
- En consecuencia, ya no será posible crear objetos de esa clase, porque las clases abstractas no son instanciables.
![[Clase abstracta.png]]