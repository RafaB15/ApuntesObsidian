- Uno diseña y modela una entidad en un **contexto**, el cual determina cuan apropiada o no es la representación que estoy haciendo.
	- En el de análisis saltamos con que una cada no tiene una alarma. Pero en el contexto del sistema que queremos resolver tiene sentido que nuestras casas puedan tener una alarma.

- **Ports y adapters ejercicio de alarma**:
	- Port era la terminal, stdin y stdout
	- Adaptador era lo que relacionaba eso con el modelo.
	- Cumplen con la arqui hexagonal?
	- Ninguna cumplía con eso porque no están modelados ports y adapters.
	- Tengo mis objetos de negocio, que tienen cierta lógica que quiero testear, y los quiero poder testear independientemente de si uso la terminal o si uso una bdd.
	- En los ejercicios no están modelados ports y adapters.
	- Como en el modelo de negocio no hay ningún put ni nada de eso a través de un port, entonces no está modelado ports y adapters.
- La mayoría entendió por arq hexagonal que no se hagan puts en el modelo.
- Ports y adapters en job vacancy:
	- Branch de billing
	- modales offer counter, se le pueden pasar repositorios.
	- En los tests se le pasa un oduble de prueba.
	- En la aplicación se crea un repositorio de verdad y se le pasa un repositorio de verdad.
	- Si no lo recibiéramos como parámetro, no podríamos usar doubles.

# Escalabilidad

- No tiene que ver con las funcionalidades que puedo agregar.
- Tiene que ver con el consumo de recursos
- Si yo quiero que porcese el doble de transacciones por segundo, le tendremos que dar más recursos.
- Ante la variación de la carga, cómo varía la escalabilidad de recursos.
- Si no escala, si tengo muchas más transacciones, por más que le agregue recursos, no va a mejorar.
- Mínimamente queremos que sea lineal.
- Tenemos que hacer pruebas de performance.
- La clase debe estar cerrada para cambios, y abierta para extensión.
- La parte de ofertas no tiene paginado.
	- Esa página no escala, porque si tuviéramos 3 millones de ofertas la página tardaría muchísimo en cargar. No escala.


- Problema no cumple abierto cerrado/código repetido. Problema
- Si no usa herencia o polimorfismo es anecdótico, no es un problema


# Hosting

- A diferencia de una compu que usamos para trabajar, los servidores son máquinas que hostean y resuelven pedidos.
- Para servidores tenemos sistemas operativos de servidor. Windows server, ubuntu server.
	- No tiene interfaz de usuario.
	- Suelen tener restricciones de seguridad y demás.
	- Es poco habitual tener un único servidor físico. Sino que se tienen muchos servidores y tenemos una máquina virtual, y nuestra aplicación corre sobre la máquina que usa todos los servidores. 
- Infrastructure as a service
	- La máquina virtual la tenemos en la nube. Amazon
	- Entonces levantamos la máquina virtual y listo. Instalarle todo es nuestra responsabilidad, pero no nos hacemos problemas por la cuestión del datacenter
- Platform as a service
	- El proveedor levanta la máquina virtual
	- Instala todo lo necesario.
	- Solo le tiramos nuestra aplicación y los datos.
	- Heroku, Vercell, Render
- Software como servicio.
	- No gestiono nada, solo quiero usar la aplicación

![[Pasted image 20240415093500.png]]


- Gitlab CI 
- ![[Pasted image 20240415101214.png]]
- Con cada commit se ejecuta esto
- job_deploy_staging: stage: deploy_staging script: - curl $DEPLOY_STAGING_URL\?\DEPLOY_STAGING_PARAM only: - render
- ![[Pasted image 20240415101441.png]]
- Trabajamos sobre un branch billing. Commitear hace todos los test
- No hacemos deploy con cada commit. 
- Trabajamos en el branch billing
- Tendremos otro branch (dploy) y desplegamos sobre este.
- Al hacer un merge al deploy entonces mergeamos.
- ![[Pasted image 20240415101604.png]]
- Deploy lo hacemos desde billing.
- ¿Cuándo vamos a deployar? Despues de cada ciclo grande, que pase el acceptance test.
![[Pasted image 20240415101930.png]]

- Otra opción es hacer un deploy al final de todo, pero eso es medio grande.

- Parte de manage, members y le damos el rol de mainteiner. 