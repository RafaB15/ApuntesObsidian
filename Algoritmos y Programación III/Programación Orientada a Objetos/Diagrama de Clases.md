- Se sigue el *Unified Modeling Language*, **UML**
- Representan relaciones estáticas entre clases e interfaces (no cambian a través del tiempo) 
- Una clase se representa con un rectángulo con tres divisiones: una para el nombre, otra para los atributos y otra para los métodos 
- En ocasiones no usamos las tres divisiones, sino solo dos (eliminando los atributos) o una (solo con el nombre de la clase) 
- Los atributos y métodos privados se pueden indicar precedidos de un signo -, los públicos del signo + y los protegidos del signo # 
- No es conveniente utilizar aspectos de la sintaxis que tengan un significado solo en determinado lenguaje.
![[Diagrama de clases 1.png]]
![[Pasted image 20240126234916.png]]

- El profesor tiene una colección llamada cursos y cada elemento de es colección es un Curso.

# Relaciones

Las [[Clase|clases]] tienen diferentes relaciones:


## Asociación

- Dos objetos interactúan y quedan relacionados. 
- No dependen fuertemente de la existencia del otro.

![[Pasted image 20240127184632.png]]
## Agregación

- Distintos ciclos de vida 
- Hay una dependencia
- Auto tiene a Rueda como atributo pero lo recibió por parámetro, por lo que no tienen el mismo ciclo de vida.

![[Pasted image 20240127184733.png]]

## Composición
- Tienen igual ciclo de vida 
- Los objetos contenidos no tienen sentido fuera de la clase contenedora.
- Se instancian dentro de la clase al crearla.
![[Pasted image 20240127184822.png]]
## Dependencia

- Una clase (o método) usa otro objeto o clase en alguna capacidad.

![[Pasted image 20240127184851.png]]

## Generalización

- Una superclase define atributos y comportamientos comunes, mientras que las subclases los heredan. 
- Las subclases pueden agregar o modificar lo que necesiten

![[Pasted image 20240127185008.png]]

## Realización

- Una clase abstracta/interfaz es implementada por otra clase

![[Pasted image 20240127185037.png]]