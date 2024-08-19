1, 2, 3 no hacemos
4,5 cosas que hacemos que no son parte de scrum

- No hacemos una **daily**. -> No amerita.
- No hay **scrum master**. -> Tiene que haber siempre una persona con el gorro de scrum master? No. Es un conjunto de responsabilidades. Se puede distribuir en todo el equipo. En algunas empresas hay un scrum master específico. Si hay alguien específico, qué hace afuera de las reuniones?
- No parecen haber un product goal, sprint goal muy definido.
- Por tener relación profesor y alumno con el product owner, hay una relación de jerarquía que no debería estar.

- Una persona puede tener varios roles mientras no haya conflictos de interés.
- Posibles conflictos de interés en scrum
	- Desarrollador y product owner.
	- Scrum master y product owner puede ser, porque a veces el intermediario es el scrum master.
- Desarrollador puede ser scrum master.
- Definition of Done/Ready nos falta.

- De qué tamaño son nuestra iteraciones?
	- Una semana
	- Scrum las llama sprints, no iteraciones. Son lo mismo. Lapso de tiempo fijo. En la guía pueden ser de 2 a 4 semanas.
- La iteración arranca con la planning
	- Participan el product owner, el equipo de producción y el scrum master.
	- Si hay algún usuario/stakeholder puede participar de esta reunión.
	- Dura 1 hora, o una hora por cada semana.
	- Hacemos un plan de trabajo, en el que definimos user stories (nosotros).
		- Para scrum son Product Backlog Items. Necesitan nombre y una prioridad definida por el PO. También necesitan una estimación del costo. El equipo es el que estima los tamaños / pesos.
	- (Nosotros hacemos) Se hace el example mapping. Se define el comportamiento de cada historia.
	- Qué vamos a hacer -> Interviene el PO. 
	- Parte táctica. Cómo lo vamos a hacer -> No se mete el PO.
	- En la planning hay que tener el código a mano para poder darse cuenta de cuantos archivos hay que cambiar para una story.
	- Si queremos agregar Gherkins entonces hay que hablarlo con el product owner.
	- Si un trabajo resulta ser más grande de lo que habíamos planeado, tenemos que blanqueárselo al PO para no perjudicarnos ni a nosotros ni al negocio.
	- Nosotros mandamos un mail.
	- Si el PO está entrenado, te puede caer con los Gherkins. 
	- El mail es invento de Paez. Sirve para poner contexto. Podrímaos hasta poner ahí el sprint goal si tuviéramos uno (En gitlab no se puede, Jira sí).
- Pair programming es de xtreme programming, no de scrum.
- Si hay nuevo trabajo se tiene que avisar.


Definition of Done

The Definition of Done is a formal description of the state of the Increment when it meets the quality measures required for the product.
Es una descripción del estado del incremento después de cumplir las medidas de calidad definidas por el producto
Es lo que tiene que cumplir un item del product backlog para poder considerarse que hubo un incremento.

Podemos decir que done es que esté en test, en prod o que sté en prod y el po de el visto bueno.

Defnition of Ready

“Product Backlog items that can be «Done» by the Development Team within one Sprint are deemed «Ready» for selection in a Sprint Planning”

La Definition of Ready es una técnica que consiste en definir las características que debe cumplir un item para entrar al Sprint.


Backlog general de productos -> No todos cumplen con la definition of ready
Los que están dentro de la planificación de la iteración -> Cumple con la definition of ready

Definition of ready no se meciona en scrum

Los definimos en nuestro caso con los gherkin, casos de uso.
Para la definition of ready se pueden pedir muchas cosas. Por ejemplo si estás por hacer una pantalla, podés querer pedir que se te de un boceto de la pantalla (mock up).

Tendremos que acordar un definition of ready con nuestro PO y cargarlo en la web.

Done -> Lo puse en test, PO lo vio, lo corrigió, **lo ponemos en Prod**

Accesibilidad -> Aplicación provee ciertas funciones para gente con capacidade sdisminuidas.

Nuestra review:
- Una ppt que armamos para contar qué pasó durante la iteración.
- 2da parte hacer una demo.
- La review no es un lugar para sorpresas. El po no se puede enterar que algo no está terminado en la review.
- Lo que codeamos debería andar en la demo o está desaprobado.
- Si te piden probar algo decís "El "caso pedido" no está contemplado. Después de la demo lo podemos ver".