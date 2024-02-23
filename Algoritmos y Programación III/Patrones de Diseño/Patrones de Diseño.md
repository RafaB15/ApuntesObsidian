> Cada patrón describe un problema que ocurre una y otra vez en nuestro entorno, así como la solución a ese problema, de tal modo que se pueda aplicar esta solución un millón de veces, sin hacer lo mismo dos veces
> *Christopher Alexander, 1977*

- Cada patrón nomina, explica y evalúa un diseño importante y recurrente en los sistemas orientados a objetos.
- Nuestro objetivo es representar esa experiencia de diseño de forma que pueda ser reutilizada de manera efectiva por otras personas.
- Para lograrlo, hemos documentado algunos de los patrones de diseño más importantes y los presentamos como un **catálogo**.
- Los patrones de diseño nos ayudan a elegir las alternativas de diseño que hacen que un sistema sea reutilizable, y a evitar aquéllas que dificultan dicha reutilización.

# Abstract Factory

- Proporciona una interfaz para crear familias de objetos relacionados o que dependen entre sí, sin especificar sus clases concretas.
- Las factories ayudan a que no se acoplen las diferentes clases.

# Builder

- Separa la construcción de un objeto complejo de su representación, de forma que el mismo proceso de construcción pueda crear diferentes representaciones.

# Factory Method

- Define una interfaz para crear un objeto, pero deja que sean las subclases quienes decidan qué clase instanciar. 
- Permite que una clase delegue en sus subclases la creación de objetos.

# Prototype

- Especifica los tipos de objetos a crear por medio de una instancia prototípica, y crea nuevos objetos copiando de este prototipo.

# Singleton

- Garantiza que una clase sólo tenga una instancia, y proporciona un punto de acceso global a ella.

# Adapter

- Convierte la interfaz de una clase en otra distinta que es la que esperan los clientes. 
- Permite que cooperen clases que de otra manera no podrían por tener interfaces incompatibles.

# Bridge

- Desacopla una abstracción de su implementación, de manera que ambas puedan variar de forma independiente.

# Composite

- Combina objetos en estructuras de árbol para representar jerarquías de parte-todo. 
- Permite que los clientes traten de manera uniforme a los objetos individuales y a los compuestos.

# Decorator

- Añade dinámicamente nuevas responsabilidades a un objeto, proporcionando una alternativa flexible a la herencia para extender la funcionalidad.
- Es un objeto que hereda de una clase abstracta y tiene como atributo a otro objeto que hereda de la clase abstracta. Entonces nosotros sobreescribimos algunos métodos pero si queremos hacerlos de otra forma se lo pedimos al objeto que tenemos como atributo.

# Façade

- Proporciona una interfaz unificada para un conjunto de interfaces de un subsistema. 
- Define una interfaz de alto nivel que hace que el subsistema sea más fácil de usar.

# Flyweight

- Usa el compartimiento para permitir un gran número de objetos de grano fino de forma eficiente.

# Proxy

- Proporciona un sustituto o representante de otro objeto para controlar el acceso a éste.

# Chain of Responsibility

- Evita acoplar el emisor de una petición a su receptor, al dar a más de un objeto la posibilidad de responder a la petición. 
- Crea una cadena con los objetos receptores y pasa la petición a través de la cadena hasta que ésta sea tratada por algún objeto.

# Command

- Encapsula una petición en un objeto, permitiendo así parametrizar a los clientes con distintas peticiones, encolar o llevar un registro de las peticiones y poder deshacer las operaciones.

# Interpreter

- Dado un lenguaje, define una representación de su gramática junto con un intérprete que usa dicha representación para interpretar sentencias del lenguaje.

# Iterator

- Proporciona un modo de acceder secuencialmente a los elementos de un objeto agregado sin exponer su representación interna

# Mediator

- Define un objeto que encapsula cómo interactúan un conjunto de objetos. 
- Promueve un bajo acoplamiento al evitar que los objetos se refieran unos a otros explícitamente, y permite variar la interacción entre ellos de forma independiente.

# Memento

- Representa y externaliza el estado interno de un objeto sin violar la encapsulación, de forma que éste puede volver a dicho estado más tarde.

# Observer

- Define una dependencia de uno-a-muchos entre objetos, de forma que cuando un objeto cambie de estado se notifica y se actualizan automáticamente todos los objetos que dependen de él

# State

- Permite que un objeto modifique su comportamiento cada vez que cambie su estado interno. 
- Parecerá que cambia la clase del objeto.
# Strategy

- Define una familia de algoritmos, encapsula cada uno de ellos y los hace intercambiables. 
- Permite que un algoritmo varíe independientemente de los clientes que lo usan.

# Template Method

- Define en una operación el esqueleto de un algoritmo, delegando en las subclases algunos de sus pasos. 
- Permite que las subclases redefinan ciertos pasos del algoritmo sin cambiar su estructura.

# Visitor

- Representa una operación sobre los elementos de una estructura de objetos. 
- Permite definir una nueva operación sin cambiar las clases de los elementos sobre los que opera.

# Bullet Points

- Conocer los conceptos básicos de OO no hace de uno un buen diseñador. 
- Los buenos diseños son reutilizables, extensibles y mantenibles. 
- Los patrones muestran cómo construir sistemas con buenas cualidades de diseño. 
- Los patrones son experiencia con orientación a objetos probada. 
- Los patrones no dan código, dan soluciones. Uno los aplica al producto específico. 
- Los patrones no se inventan, se descubren. 
- La mayoría de los patrones y principios abordan cuestiones de cambio del software. 
- La mayoría de los patrones permiten que alguna parte de un sistema varíe independientemente de todas las demás partes. 
- A menudo tratamos de tomar lo que varía en un sistema y encapsularlo. 
- Los patrones proporcionan un lenguaje compartido que puede maximizar el valor de la comunicación con otros desarrolladores.