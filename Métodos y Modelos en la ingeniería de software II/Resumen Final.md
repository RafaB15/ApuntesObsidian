# Proceso de construcción

## Premisas

- El desarrollo es guiado por pruebas
- El proceso es iterativo y los incrementos son pequeños.
- Integración, verificación y entrega continua.
- Mantenerlo estúpidamente simple (KISS).

# Técnicas

## BDD / TDD / DDD

- BDD: Extiende TDD al escribir tests en un lenguaje no técnico.

- TDD (Test Driven Development): teóricamente el más abarcativo, habitualmente usado como sinónimo de UTDD.
- UTDD (Unit Test-Driven Development): Centrado en especificación del diseño detallado (por ejemplo, si trabajamos en programación orientada a objetos a nivel de métodos y objetos.)
- BDD (Behavior-Driven Development): Se basa en criterios de aceptación, aunque se los denomine especificaciones de comportamiento. Se suele usar tanto para especificar requerimientos como diseño de alto nivel. Muchos lo consideran sinónimo de ATDD, STDD y SBE.
- ATDD (Acceptance Test-Driven Development): Basado en criterios de aceptación exclusivamente.
- STDD (Storytest-Driven Development) Basado en la especificación de requerimientos usando pruebas. 
- SBE (Specification By Example): Prácticamente lo mismo que STDD, aunque el foco está puesto en los ejemplos como herramienta de comunicación entre roles de especificación de criterios de aceptación en forma de ejemplos.
- Hay dos maneras de ver la calidad, una interna que les sirve a los desarrolladores y otra externa que la perciben los clientes y usuarios. UTDD y TDD apuntan más a calidad interna, BDD, ATDD y STDD apuntan a la externa.

- Ciclo TDD
- Ciclo chico: Escribe un test unitario que falle, escribe un poco de código para que el test pase, refactoriza el código para que sea una implementación de las features testeadas tan simple como sea posible. Repetí.
- Ciclo grande: Se escribe un test de aceptación que falle, se hace el ciclo chico hasta que pase el test, repetir.
![[Pasted image 20240627190333.png]]
- Tipos de test por Freeman:
	- **Aceptación**: Funciona el sistema entero?
	- **Integración**: Nuestro código funciona con código que no podemos cambiar?
	- **Unitario**: Nuestros objetos hacen lo correcto? Es conveniente trabajar con ellos?
- Test end-to-end
	- Los tests end to end interactúan con la aplicación únicamente a través de su interfaz de usuario, como mandando mensajes como un sistema third party.
- Es bueno testear comportamiento, no métodos.
- Cuando el diseño es difícil de testear es un indicativo de que nuestro diseño está mal.

![[Pasted image 20240627223715.png]]
## Integración continua
## Walking Skeleton

- Construir un walking skeleton es una buena forma de empezar el proceso de testeo cuando no sabemos por donde empezar.
- Un walking skeleton es una implementación del pedazo de funcionalidad más pequeño posible que podemos contruir, deployar, y testear end-to-end automáticamente.
- Primero construimos, deployamos y testeamos un walking skeleton. Leugo usamos esa infraestructura para escribir tests de aceptación para la primera feature importante. 

![[Pasted image 20240627190420.png]]
## Arquitectura Hexagonal

- También conocida como puertos y adaptadores.
- El código de lógica de negocio está aislado de sus dependencias técnicas en la arquitectura, como bases de datos e interfaces de usuarios.
- No queremos conceptos técnicos en el modelo de la aplicación, por lo que se escriben *interfaces* para describir la relación con el mundo exterior en terminología del negocio (PUERTOS).
- Luego escribimos puentes entre el núcleo de la aplicación y todo dominio técnico (ADAPTADORES). Estas implementan la interfaz definida por el modelo de la aplicación y mapean de objetos de nivel de aplicación a nivel técnico.

![[Pasted image 20240627222252.png]]

## Estilo Orientado a Objetos

### Separación de incumbencias

- Cuando queremos cambiar el comportamiento de un sistema, queremos cambiar la menor cantidad de código posible.
- Como no podemos anticipar cuando tendremos que cambiar una parte específica del sistema, agrupamos junto código que cambiaría por la misma razón.
### Niveles más altos de abstracción

- Lidiamos con la complejidad a través de las abstracciones.
- Realizamos más si programamos combinando componentes de funcionalidad útil en vez de manipulando variables y flujos de control.
- Cada objeto debería tener una única y claramente definida responsabilidad. (Single Responsibility Principle)

Siguiendo estas heurísticas llegamos a algo parecido a los puertos y adaptadores de Cockburn.


# Gestión de proyectos

- Proyecto: Emprendimiento **temporal** para la provisión de un **servicio / producto** particular bajo ciertas **restricciones**.
	- Dimensión temporal.
	- Fin del proyecto.
	- Restricciones en las que ocurre.

![[Pasted image 20240630125343.png]]

- Son las variables de control de proyecto y se las conoce como triangulo de acero. Normalmente: El cliente determina el alcance, el proveedor determina los recursos y el calendario queda como variable de ajuste / negociación.
- Fases:
	- **Inicio**: Le damos forma, definimos una visión, se ponen los riesgos sobre la mesa, se define el presupuesto, confirmamos que haremos el proyecto.
	- **Organización**: Organizamos para empezar a ejecutar el proyecto. Armado de equipo, compra de licencias, capacitación.
	- **Ejecución y control**: Empezamos a codear con algún proceso elegido.
	- **Cierre**: Puede tomar distintas formas. Transferencia de conocimiento a un equipo de soporte por ejemplo.
- Roles:
	- **Sponsor**: Pone la plata, no necesariamente es el usuario.
	- **Usuario**: Es el que va a usar el proyecto, a veces no es el sponsor.
	- **Equipo de especialista**s: Los que lo hacen.
	- **Stakeholders**: Aquellos que tienen algún interés en el producto o servicio.
- Formas de contratación / venta:
	- Llave en mano: El contratante determina alcance, el proveedor un precio para este alcance y lo que varía es el esfuerzo del proveedor.
		- Fix Price
		- Alcance y Precio fijos
		- Esfuerzo Variable
	- Tiempo y materiales: El cliente no tiene en claro lo que quiere construir, entonces vamos explorando lo que hay que hacer y cobro por el tiempo.
		- Times & Materials
		- Alcance variable
		- Precio hora fijo

# Planificación

- Elementos para la planificación:
	- Trabajo a trabajar (WBS, backlog o similar)
	- Disponibiliad de recursos / personas / capacidad / velocidad
	- Restricciones de tiempo / fechas.
- Planificar implica
	- Estimar
	- Estableces el tamaño de iteración (1 o 2 semanas)
	- Establecer fechas tentativas de release (Después de cuantas iteraciones hacemos la primer release y cada tanto actualizamos)
	- Identificar riesgos.
- Equipos chicos normalmente.
- A veces se hace un primer release (MVP) y luego se hace entrega continua.
- Cada item del backlog tiene que cumplir con:
	- Tiene que tener una prioridad asignada por el PO / gente de negocio.
	- Una primera estimación de tamaño hecha por el equipo de desarrollo.
- Podemos tener items grandes en el backlog mientras que no lo tengamos en la iteración. Al querer ponerlo en la iteración habrá que particionarlo para que sean más pequeños, que podamos completarlo en una iteración. La suma de las partes puede tener más peso que el item inicial. Al partirlo hay que volver a priorizar.
- En xp se debería hacer al menos 6 ítems por iteración.

# Estimación

- Variables:
	- Tamaño / Complejidad
	- Esfuerzo
	- Tiempo
	- Costo
- Tipos de métodos:
	- Paramétricos: Se realizan conteos y se hace una fórmula con esos parámetros. Eso genera un número.
		- COCOMO
		- COSYSMO
		- COCOMO II
	- Basados en opiniones: La gente dice qué opina acerca de lo que hay que construir.
		- Delphi
		- Wideband Delphi
		- Planning Poker
- Estimación relativa
	- Suele ser más simple
	- Buscamos el item más pequeño y lo establecemos como unidad (1 story point)
	- Luego ponemos el resto de los ítems en relación a la unidad.
- Usamos Yesterday's Weather para elegir la cantidad de story points que haremos una iteración, comprometiéndonos a hacer tantos items como logramos hacer la iteración pasada.
- Spike: 
	- Item de backlog con el agregado para despejar la incertidumbre sobre otro ítem del backlog.
	- Debe generar como output la estimación del ítem original.
	- Suele incluir la realización de una prueba y/o investigación.
- Slack
	- Estrategia para manejo de imprevistos. Si sabemos que tenemos una velocidad de 15 puntos, no comprometemos esos 15 puntos, por ahí hacemos 14 y comprometemos un punto como slack. No lo dejamos flotando, pero lo contamos como slack. Llenamos ese punto con alguna tarea de baja prioridad y tranqui.
	- Inicialmente planificado para tareas de baja prioridad
	- Deuda técnica / Refactoring / Investigación

# Métodos Ágiles

- Manifiesto ágil
	- Estamos encontrando mejores formas de desarrollar software y ayudar a otros a que lo hagan.
- 4 valores
	- Individuos e interacciones sobre procesos y herramientas.
	- Software funcional sobre documentación comprensiva.
	- Colaboración con el cliente sobre negociaciones contractuales.
	- Responder al cambio sobre seguir un plan.
- 12 principios
	- Nuestra prioridad más alta es satisfacer al cliente a través de una entrega temprana y continua de software valioso.
	- Bienvenimos requerimientos cambiantes, incluso tarde en el desarrollo. Los procesos ágiles utilizan el cambio para la ventaja competitiva del cliente.
	- Entrega software funcionando constantemente, desde un par de semanas hasta un par de meses, prefiriendo los espacios de tiempo más cortos.
	- Las personas del negocio y los desarrolladores debe trabajar juntos diariamente a lo largo del proyecto.
	- **Construye proyectos alrededor de individuos motivados. Dales el ambiente y soporte que necesitan y confía en ellos para llevar a cabo su trabajo.**
	- El método más eficiente y efectivo para transmitir información a un y dentro de un equipo de desarrollo es una conversación cara a cara.
	- El software funcionando es el medidor primario del progreso.
	- Los procesos ágiles promueven el desarrollo sostenible. Los sponsors, desarrolladores y usuarios deberías ser capaces de mantener un ritmo constante indefinidamente.
	- **La atención continua a la excelencia técnica y al buen diseño mejoras la agilidad.**
	- La simplicidad, el arte de maximizar la cantidad de trabajo no hecho, es esencial.
	- **Las mejores arquitecturas, requerimientos y diseños emergen de equipos auto organizados.**
	- **En intervalos regulares, el equipo reflexiona en cómo ser más efectivos, luego tunean y ajustan su comportamiento adecuadamente.**
- Más allá del manifiesto ágil, los métodos ágiles tiene los siguientes puntos en común:
	- Proceso iterativo y time-boxed
	- Retrospectivas
	- Entrega frecuente
	- Propiedad compartida
	- Auto organización
	- Diseño emergente
	- Pruebas automatizada
	- Integración continua
	- Test-Driven Development
	- Programación de a pares
- Si no hay muchas incertidumbres en el proyecto ni cambios y sabemos muy bien lo que tenemos que hacer, los métodos ágiles a veces no nos suman demasiado. Pero igual los podemos utilizar y no nos restan.
- Cuando SI utilizarlos
	- Alto involucramiento del cliente / usuario
	- Bajo costo de iteración
	- Gente preparada / "Bajo juniority"