- Manifiesto que expone 12 principios que deberían tenerse en cuenta para construir aplicaciones.
- Foco en arquitectura e infraestructura.
- Foco en la calidad.
# Codebase
- **Código base**
- Un sólo código múltiples deploys
- El código en la aplicación debe gestionarse con un sistema de control de versiones (como git).
- Relación 1 a 1 con la aplicación.
- Múltiples códigos base -> sistema distribuido
- Si nuestro sistema está separado en front, back o trabajamos con microservicios, tendremos muchos repositorios en los que podremos aplicar estos 12 principios por separado.
- Se pueden usar para hacer deploy en ambientes variados.
	- El código siempre es el mismo, pero en diferentes versiones se puede estar viendo una versión distinta del código (como cuando tenemos deploys de diferentes ramas).

# Dependencias
- Declarar y aislar explícitamente las dependencias.
- En un gemfile o pyfile encontramos las librerías que vamos a necesitar.
- Se pueden instalar en el sistema o el directorio que contiene la aplicación.
- Si mi aplicación no corre solamente en mi ambiente local, tendremos que también tener nuestras dependencias en el  servidor que uso para producción.
	- Siempre tenemos que declarar un **manifiesto** de nuestras dependencias y ejecutar mi aplicación aisladamente.
	- Los lenguajes de programación suelen tener bundlers, donde se ejecuten y apliquen las librerías declaradas.

# Configuraciones

- Guardar la configuración en el entorno.
- Una aplicación que requiere una base de datos necesitará credenciales para identificarse. 
- Para ambientes fuera de mi computadora mi entorno también tendrá que poder conectarse a al base.
- En padrino dependiendo de la variable de entorno, podemos settear qué varaibles de entorno buscar y las setteamos en el entorno nuevo.
- Estricta separación de código y configuración
	- Lo único que cambia de un deploy a otro son las variables de entorno
	- Por eso se desalienta el uso de archivos property/env.
- Clasificación: local, stage, production
	- En nuestra app, el código que hace un switch dependiendo de la variable de ambiente no es una buena práctica, porque supone que para cada nuevo deploy habrá que tocar el código.
- ¿Qué ocurre si decido que mi codebase sea público?
	- Si hacemos un código público no hay que comprometer ninguna credencial o dato sensible de nuestra aplicación.

# Backing Services
- Tratar a los backing services como recursos conectables
- Se llama así cualquier recurso de aplicación que es consumido a través de la red como parte de un funcionamiento habitual
	- Base de datos (MySQL)
	- Servicio de mailing
	- Amazon S3
- Está muy vinculada a la aplicación.
- Se propone que se trate a estos recursos como recursos conectables, y que mi código no se entere de exactamente qué hay debajo del servicio.
	- En nuestro código en gestión por ejemplo, el front llama a los controllers, y los controller/routers(?) se comunican con la base de datos PostgressSQL. Pero si mañana quiero cambiar a MySQL, el front no se entera, sino que cambio los controllers

# Build, Release & Run
- Separar completamente la etapa de construcción de la etapa de ejecución.
- Para que la codebase se transforme en un deploy habrá que completar 3 etapas.
	- Construcción
		- Transformar el código en un paquete ejecutable llamado build
		- Aquí se descargan todas las dependencias y se compilan los binarios usando una versión específica del codebase.
	- Distribución
		- Combinamos el paquete recién construido con la configuración (que tenía que estar separada).
		- Generamos una distribución llamada release.
	- Ejecución
		- Se toma el release y se ejecuta en un entorno específico.
- Estas etapas deben estar estrictamente separadas.
- Hay herramientas para esto, como Capistrano, pero muchos usan herramientas custom.
- Se deben tener identificadores únicos de las distribuciones
	- Timestamp
	- Número Incremental
- Las distribuciones son como un libro de contabilidad, puedo agregar nuevos pero no modificar los que ya están. Habría que hacer un nuevo release.
# Procesos
- Ejecutar la aplicación como uno o más procesos sin estado.
- Cuando un usuario quiere acceder a un recurso de mi aplicación, esta puede lanzar un proceso. Lo procesos que tenga que generar la respuesta se propone que sean del tipo stateless y share nothing.
- Las aplicaciones deben lanzar procesos:
	- Stateless
		- Es independiente de otras peticiones que puede estar recibiendo la aplicación.
		- Por ejemplo, si hay una variable compartida entre procesos que vamos aumentando, el número de esa variable depende de las otras peticiones siendo contestadas. Esto es candidato a quedar en un backing service para no cargar a nuestro proceso con esa responsabilidad.
	- Share nothing
		- Cada ejecución tiene su propio espacio en disco, designación de memoria y procesamiento de CPU aislado.
		- La correcta ejecución de mi aplicación no puede depender de que tenga cosas compartidas.
		- No deberían acceder a los mismos ficheros para leer y escribir por ejemplo.
# Asignación de puertos
- Publicar servicios mediante asignación de puertos
- Cuando levantamos una aplicación web en nuestro entorno local la tendremos en localhost:puerto.
- La URL en un ambiente no local será la IP del servidor en cuestión y para identificar a nuestra aplicación dentro de este servidor, necesitaremos un puerto específico.

# Concurrencia

- Escalar mediante el modelo de procesos.
- Procesos: ciudadanos de 1era clase
	- Tienen una entidad en sí misma
	- Son un componente especial dentro de la aplicación.
	- Si lo llevamos al lenguaje de objetos, son una clase abstracta y tendrán muchas implementaciones.
- Modelo de procesos
	- Tipo: 
		- Web: Atienden peticiones web
		- Worker: Hacen trabajo de cálculo y procesamiento para conseguir una respuesta
		- Clock: Acciones que necesitamos que se ejecuten a un determinado horario.
	- Carga
		- Cada tipo de proceso de nuestra aplicación va a tener una diferente carga de trabajo
		- Si seguimos el modelo stateless y share nothing, para escalar la escala habrá que tener más procesos de los mismo tipos.
- El aumento de la concurrencia
	- No tendrá riesgos
	- Será simple

![[Pasted image 20240512231901.png]]

# Desechabilidad

- Hacer el sistema más robusto intentando conseguir inicios rápidos y finalizaciones seguras.
- Inicio de procesos:
	- Rápido (si seguimos lo que venimos planteando)
	- Flexible
		- Escalar el procesamiento en cualquier momento.
		- ubicar de manera segura los recursos que se requieran
		- Deploys
		- Cambios de configuraciones
- Finalizar el proceso
	- Flujo normal: Se recibe una petición, se procesa, se da una respuesta, se termina el flujo.
	- Señal SIGTERM - Seguro
		- Colas de trabajo-
		- Se busca detener un proceso de forma segura aunque este no haya terminado.
	- Crash / Fallo de Hardware
		- Hay que intentar que nuestro entorno se pueda recuperar de este tipo de fallas.
	- En conclusión, **los procesos deben ser desechables**. No podemos depender de que una ejecución termine bien para que mi sistema sea estable. Esto nos brinda una gran capacidad de resiliencia.

# Paridad en desarrollo y producción

- Mantener desarrollo, preproducción y producción tan parecidos como sea posible.
- Tiempos entre despliegues menos.
- Cercanía entre desarrollo y operaciones acentuada.
- Los servicios y herramientas son replicados en producción como funcionan en desarrollo.

# Logs

- Tratar los logs como una transmisión de eventos.
- ¿Dónde se almacenan? A la aplicación no le debería importar, solo al entorno de ejecución, quien debería redirigir de salida estándar al archivo de log.
- Si se configura donde guardar los logs, se sabe como acceder a ellos.

# Administración de procesos
- Ejecutar las tareas de gestión / administración como procesos que solo se ejecutan una vez.
- Procesos de adminsitración /mantenimiento
	- Migrations
	- Scripts
- Son lanzados a drede por un administrador o desarrollador.
- Cualquier tipo de proceso debe correr bajo las mismas reglas que cualquier tipo de aplicación.
- Se recomienda lenguajes de programación que proporcionan consolas de tipo REPL que se ejecutan y corren solo una vez (python y ruby tienen consolas interactivas).