- La arquitectura hexagonal, o arquitectura de puertos y adaptadores, es un patrón arquitectónico usado en el diseño de software.
- Apunta a crear componentes de las aplicaciones que no estén muy acoplados que se pueden conectar a un ambiente de software fácilmente a través de puertos y adaptadores.
- Esto vuelve a los componentes intercambiables en cualquier nivel y facilita la automatización de los tests.
- La idea de la arquitectura hexagonal es la de poner las entradas y salidas en los extremos del diseño. La **lógica de negocio** no debería depender de si exponemos una API REST o GraphQL, y no debería depender de donde conseguimos los datos (una base de datos, una API de microservicios expuesta a través de gRPC o REST, o un archivo CSV simple).
- Vemos que con la arquitectura hexagonal las dependencias van hacia adentro, haciendo que sea fácil cambiar nuestra lógica de negocio.

![[Pasted image 20240406174509.png]]

- La lógica del negocio que estamos modelando está en el centro, y no tiene ninguna dependencia con la infraestructura y la entrada / manejo de entrada salida de información.
- Tenemos puertos y adaptadores para que se comunique con estos.
- Clean architecture se basa en esto.