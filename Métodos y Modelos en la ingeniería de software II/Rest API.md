# API

- Un programa que provee servicios a otros programas.
- Conjunto de definiciones e interfaces que permite interactuar a dos aplicaciones.
- Software que provee servicios a otro software.
- Las bibliotecas que usamos en el código tiene una interfaz para usarla.
- Podemos ver una API como la combinación de dos partes:
	- Qué hace (público) -> Interfaz
	- Cómo lo hace (privado) -> Implementación
# Web APIs
- Son lo mismo que las APIs, pero (en general) a través de HTTP.
- En general no se ejecutan en la misma computadora que hace la llamada a la API.
- También exponen una interfaz para que sea utilizada por los clientes.
- No hay restricciones sobre interfaz ni sobre implementación (más allá de lo impuesto por HTTP).
# REST

- **R**epresentational **S**tate **T**ransfer.
- Es una propuesta arquitectónica para el **diseño** de sistemas.
- No es único para APIs.
- REST se construye en torno a un concepto central: **recursos**.
	- Un recurso es una **abstracción** de información a la que le podemos poner un nombre.
		- Tienen una **representación**, que muestra el **estado** del recurso (JSON por ejemplo).
		- Se accede a recursos y se los modifica mediante **métodos.**
- Se basa en seis restricciones de arquitectura que se deben cumplir para poder decir que una API es **restful**.
	- **Client Server:** Mantener la interfaz de usuario (cliente) separada de los datos (servidor). Los clientes solo deberían conocer las URIs de los recursos.
	- **Stateless:** Todas las requests de los clientes deben contener toda la información para que sea comprendida, sin tomar ventaja de requests anteriores.
	- **Cacheable:** Los clientes pueden cachear respuestas, las cuales **deben** identificarse como cacheables.
	- **Layered System**: Distribuir el sistema en capas, de manera que una capa no pueda ver más allá de la capa inmediatamente debajo.
	- **Code on demand**: Opcional. Permite al server enviar código ejecutable a los clientes (ej: script tag ejecuta javascript)
	- **Uniform interface:** Mantener una interfaz uniforme a lo largo de todo el sistema para el acceso a recursos.
		- **Identificación de resursos:** Los recursos deben tener un identificador.
		- **Access methods have the same semantics:** Eg: GET, POST, etc (en HTTP).
		- **Manipulation of resources through representations:** los recursos se manipulan utilizando su representación.
		- **Self-descriptive messages:** Un mensaje contiene toda la información necesario para comprenderlo.
		- **HATEOAS (hypermedia as the engine of application state)**: Las respuestas de los recursos deberían incluir links para obtener información relacionada.
# REST APIs
- Es una api web, por lo que usa HTTP, que cumple con las 6 restricciones que plantea REST.
- Las restricciones de REST se llevan bien con HTTP.
- Están basadas en recursos. Si estamos modelando recursos es más fácil hacer una api rest. Si no, capaz tendríamos que usar una api graphql.

## Recursos y Métodos

- Los métodos son los que nos permiten acceder a recursos y actualizarlos para modificar su estado.
- Dos partes.
	- **URI:** ruta en la que se accede a un recurso. Se deben usar sustantivos para describir rutas. Ej: /clientes/{id_cliente}/cuentas.
	- **Método HTTP:** Rest no define relación entre métodos HTTP y los que deberían usarse en REST (pero se usan convenciones).

![[Pasted image 20240519153407.png]]
![[Pasted image 20240519153533.png]]
## Seguridad
- Control de acceso:
	- JWT
	- API keys
- HTTPS
- Evitar exponer información sensible
	- Manejo de errores
	- Información en requests
- Validación de input
# Especificación
- Es muy importante que la implementación haga lo que la API promete.
- La forma de comprometerse es a través de la especificación -> indica qué hace cada endpoint y cómo utilizarlo.
- Un cliente debería ser capaz de utilizar la API a través de su especificación (y de la información que devuelve al utilizarla)

## Open API
- Forma bastante popular de documentar una API
- Archivos YML