- Arquitectura en capas
	- Interfaz de usuario
	- Aplicación
	- Dominio
	- Infraestructura

![[Arquitectura en capas.png]]

- A diferencia de esta imagen, la de infraestructura en realidad es medio transversal al medio de las capas
- **Servicios**:
	- De dominio:
		- Tienen lógica de negocio.
		- No tiene ninguna relación con la infraestructura.
		- Sirve para poner lógica que no calza en ningún objeto de mi entidad. La ponemos en un objeto de servicio.
	- De aplicación:
		- Tiene lógica de alto nivel que tiene que ver con mi aplicación en particular.
		- Serán objetos que tendrán la granularidad necesaria para representar una transacción del usuario coordinando distintos objetos de mi dominio (puede ser hasta el login).
	- De infraestrucutra:
		- Librerías que va a utilizar nuestra aplicación
		- La persistencia es un servicio de infraestructura
- **Repositorios**:
	- No tienen lógica de negocio, pero se encargan del ciclo de vida de los objetos que creemos.
	- Interface del repositorio: Es parte del dominio, porque este define como es el repositorio.
	- Implementación: Esto pertenece a la arquitectura, porque puede usar SQL, mongo, u otras cosas.
	- La infraestructura implementa la interfaz, se puede cambiar sin que nos enteremos.
	- No tienen lógica de negocio, solo manejan el ciclo de vida de los objetos luego de su creación.
	- El usuario no debería hacer validaciones de datos. Le podemos poner constraints, pero estas se tienen que validar en el código de la aplicación.
	- Puede sonar a duplicar lógica, pero en realidad es mantener la consistencia.
		- Si la nueva validación rompe lo que ya estaba en la base de datos a veces no te dejará agregarlo, pero en el negocio sí se podría.
- **Model-View-Controller**
	- Separación de los objetos de nuestra aplicación para tener más libertades.
	- Nos ayuda cuando tenemos una aplicación interactiva. El usuario hace algo el programa responde.
	- El usuario hace algo a partir de una vista, el usuario genera una acción que es interpretada por un controller que la traduce en un mensaje al modelo, el modelo se modifica y la vista refleja el nuevo estado del modelo.
	- Controllers
		- Están muy atados a la arquitectura.
		- Lógica difícil de testear.
		- Tentadores para poner lógica de negocio.
		- Generalmente están atados a la tecnología.
		- Puede tener lógica, pero no la que es central del problema, del negocio.
		- En el controller de job vacancy (juega el rol de adaptador web) se chequea si la password y password confirmation sean iguales porque no es lógica del negocio.
- Cómo usamos MVC y DDD?
	- User Interface -> View
	- Domain -> Model
	- Que es controller? Es UI o application?
	- Model incluye aplicación??
- **Capa de aplicación**
	- Controller 
		- Que la application layer esté encapsulado en los controllers
		- Poco conveniente porque suelen estar acoplados a la infraestructura
		- Trae muchos problemas. 
	- Application Facade
		- Clase que actúa como fachada de mi negocio y provee métodos para comunicarnos.
	- Commands/Actions
		- Cada transacción tenerla representada en una clase que representa la transacción del usuario y hace la coordinación de objetos para llevarla a cabo.
	- Services
		- Tener una capa de servicios de aplicación que provean métodos con granularidad de negocio.
	- La aplicación debería ser usable sin las pantallas

- Llamar a un objeto servicio no describe mucho. Es preferible no usarlo. Significa 50 cosas distintas.
	- Servicio SOA
	- Servicio de negocio
	- Servicio de infraestructura

- En los gherkin no es correcto poner "click" porque eso es el comportamiento de las pantallas, mientras que deberíamos describir el comportamiento de negocio.