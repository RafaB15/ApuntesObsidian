# Exclusión Mutua Distribuida

Software distribuido -> Está en múltiples computadoras ejecutándose a la vez.

## Algoritmo Centralizado

1. Un proceso es elegido coordinador.
2. Cuando un proceso quiere entrar a la sección crítica, envía un mensaje al coordinador.
3. Si no hay ningún proceso en la SC, el coordinador envía OK; si hay, el coordinador no envía respuesta hasta que se libere la SC.

## Algoritmo Distribuido

Cuando un proceso quiere entrar en una sección crítica, construye un mensaje con el nombre de la sección crítica, el número de proceso y el timestamp. Al recibir el mensaje:
1. Si no está en la SC y no quiere entrar, envía OK.
2. Si está en al SC, no responde y encola el mensaje. Cuando sale de la SC, encía OK.
3. Si quiere entrar en la SC, compara el timestamp y gana el menor.

No hay un líder, hay un consenso entre todos.
## Algoritmo Token Ring

- Se conforma un anillo mediante conexiones punto a punto 
- Al inicializar, el proceso 0 recibe un **token** que va circulando por el anillo
- Sólo el proceso que tiene el token puede entrar a la SC
- Cuando el proceso sale de la SC, continua circulando el token
- El proceso no puede entrar a otra SC con el mismo token


# Cliente Servidor

## Sockets

- Permiten la comunicación entre dos procesos diferentes
	- En la misma máquina
	- En dos máquinas diferentes
- Se usan en aplicaciones que implementan el modelo cliente-servidor:
	- Cliente: es activo porque inicia la interacción con el servidor.
	- Servidor: Es pasivo porque espera recibir las peticiones de los clientes.

## Arquitectura cliente-servidor

- Arquitectura de dos niveles: el cliente interactúa directamente con el servidor.
- Arquitectura de tres niveles: middleware
	- Capa de software ubicada entre el cliente y el servidor.
	- Provee principalmente seguridad y balanceo de carga.
- Tipos de servidor
	- Iterativo: atiende las peticiones de a una a la vez
	- Concurrente: puede atender varias peticiones a la vez.

# Comunicación

## Tipos de Sockets

- Stream sockets: usan el protocolo TCP: entrega garantizada del flujo de bytes
- Datagram Sockets: usan el protocolo UDP: la entrega no está garantizada; servicio sin conexión.
- Raw sockets: Permiten a las aplicaciones enviar paquetes IP.
- Sequenced packet sockets: similares a stream sockets, pero preservan los delimitadores de registro. Utilizan el protocolo SPP (Sequenced Packet Protocol.)
![[Pasted image 20240521113714.png]]