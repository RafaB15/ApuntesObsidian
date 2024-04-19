# Bad smell: Principios y heurísticas

Bad Smell $\to$ algo anda mal.
Si vemos varios ifs anidados, hay que ver qué está fallando.

[[SOLID]]
[[Algoritmos y Programación III/Principios de Diseño/Principios de Diseño|Principios de diseño de essaya]]

**Modelo:** Abstracción que representa un subconjunto de la realidad.
**Software:** Modelo computable del dominio de un problema.

![[Modelos software.png]]

**Funcional:** Qué tan buena es la representación del dominio.
- Novedad en el dominio $\to$ Novedad en el modelo.

**Descriptivo:** Qué tan simple es de entender, comunicar y cambiar.
- Lenguaje Ubicuo (universal). 
	- Vamos al código y encontramos las entidades de la realidad. 
	- Mismo lenguaje en el código.
	- Lenguaje depende del cliente.
- Especial importancia de los nombres.
	- Las variables tienen que tener nombres muy descriptivos.

# Domain Driven Design

- No solo podemos sentarnos y ponernos a codear. Lo podemos hacer, y funciona para casos triviales. Pero no podemos crear software complejo de esa manera.
- Modelos anémicos:
	- Clase / Objeto relevantes al dominio pero que no ejecutan lógica de dominio. (Entidad con solo un atributo)
- Usar un lenguaje común basado en el domino del problema.
- Arquitectura en capas:
	- En la capa de dominio se definen las cosas que tienen que ver con el dominio del problema.
	- Application está más relacionados a los distintos frameworks que usamos con el lenguaje. O cosas del servidor. Configuración de cómo corre la aplicación.
	- User interface es lo que ve el usuario.
	- Lo importante es que estén separados, no ese tipo de cosas en un mismo archivo.

![[Capas.png]]
- Arquitectura hexagonal es una manera de hacer esta separación.
	- No es tan lineal.
	- Lo que plantea es que lo visual (interfaces) pueden entrar por distintos lados pero el dominio se lo banca.

![[Arqui hexagonal.png]]