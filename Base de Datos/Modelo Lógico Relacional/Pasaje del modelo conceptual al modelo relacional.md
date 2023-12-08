
Se siguen las siguientes técnicas para poder pasar del [[Base de Datos/Modelo Conceptual de BDD/Modelo Conceptual|modelo conceptual]] al [[Base de Datos/Modelo Lógico Relacional/Modelo Relacional|modelo relacional]]
# Principios

- Cada [[Base de Datos/Modelo Conceptual de BDD/Entidades|entidad]] del [[Base de Datos/Modelo Conceptual de BDD/Modelo Entidad-Relación|modelo ER]] producirá generalmente una [[Base de Datos/Modelo Lógico Relacional/Modelo Relacional#Relación|relación]] del modelo relacional.

![[Base de Datos/Modelo Lógico Relacional/images/Untitled.png|Untitled]]

- Dependiendo de como modelicemos las diferentes relaciones se va a agregar o quitar restricciones.

## Atributos multivaluados

![[Base de Datos/Modelo Lógico Relacional/images/Untitled 1.png|Untitled]]

En este caso un [[Base de Datos/Modelo Conceptual de BDD/Atributos|atributo]] puede tener más de un valor. Una forma de representar esto es tomando los atributos multivaluados y creando una nueva tabla por cada uno, en donde tengamos el legajo del médico como llave foránea y la combinación de o legajo médico y teléfono o legajo médico y mail como llave primaria. De esta forma cada médico puede tener varios mail y celulares.

## Atributos compuestos

![[Base de Datos/Modelo Lógico Relacional/images/Untitled 2.png|Untitled]]

Para los atributos compuestos tomamos cada valor dentro de este y lo ponemos en su propio atributo (columna).

## Cardinalidad N:M

![[Base de Datos/Modelo Lógico Relacional/images/Untitled 3.png|Untitled]]

Cada [[Base de Datos/Modelo Conceptual de BDD/Interrelaciones|interrelación]] de mucho a muchos del modelo ER producirá un relación del modelo racional.

Creamos una tabla separada en donde poner los valores de las dos claves primarias, así como de cualquier información extra que tenga la relación. Las claves primarias que pongamos en esta tabla serán ahora llaves foráneas y la combinación de estas será la llave primaria.

## Cardinalidad 1:1

![[Base de Datos/Modelo Lógico Relacional/images/Untitled 4.png|Untitled]]

### Forma 1

Hacemos una nueva tabla con las dos claves primarias como atributos, eligiendo a una como clave primaria de la tabla y dejando a la otra como clave candidata

![[Base de Datos/Modelo Lógico Relacional/images/Untitled 5.png|Untitled]]

### Forma 2

Recomendada si una de las entidades tienen participación total

![[Base de Datos/Modelo Lógico Relacional/images/Untitled 6.png|Untitled]]

![[Base de Datos/Modelo Lógico Relacional/images/Untitled 7.png|Untitled]]

Una interrelación con cardinalidad 1:1 puede representarse incluyendo la clave primaria de una de las entidades participantes como clave foránea en la relación correspondiente a la otra entidad participante, siempre que esta última tenga participación total. Recordemos que las claves foráneas (a menos que se las restringa) pueden tener valores nulos.

### Forma 3

Cuando ambas tienen participación total

![[Base de Datos/Modelo Lógico Relacional/images/Untitled 8.png|Untitled]]

Podemos elegir cualquiera de las claves primarias del modelo ER como clave primaria de la tabla, la otra queda como clave candidata. 

En este caso se tiene la posibilidad de tener una única tabla que represente todo.

## Cardinalidad 1:N

![[Base de Datos/Modelo Lógico Relacional/images/Untitled 9.png|Untitled]]

Si el futbolista tuviera participación total

![[Base de Datos/Modelo Lógico Relacional/images/Untitled 10.png|Untitled]]

## Entidades débiles

![[Base de Datos/Modelo Lógico Relacional/images/Untitled 11.png|Untitled]]

Completamos en la tabla de la entidad débil con la clave primaria de la entidad de la cual depende para poder conseguir una combinación de atributos que nos sirva como llave primaria.

## Generalización/Especialización

![[Base de Datos/Modelo Lógico Relacional/images/Untitled 12.png|Untitled]]

Al cada persona tener que ser sí o sí una persona podemos hacer una tabla por cada especialización y referirnos a la tabla de persona a través de una llave foránea. Como es también superpuesta, en las tablas de alumnos y docentes se pueden repetir las personas sin problema.

Otra opción, en caso de que la especialización sea 

## Unión

![[Base de Datos/Modelo Lógico Relacional/images/Untitled 13.png|Untitled]]

En este caso, como la especialización va de abajo hasta arriba, tendremos que crear una ***clave subdrogada*** para identificar a los clientes. El problema de este modelo es que no logramos representar que un cliente no puede ser a la vez una persona física y una jurídica.

## Interrelaciones ternarias

### Cardinalidad N:N:N

![[Base de Datos/Modelo Lógico Relacional/images/Untitled 14.png|Untitled]]

Podemos hacer una nueva tabla con las 3 claves primarias como claves foráneas y su conjunto como la llave primaria.

## Cardinalidad 1:N:N

![[Base de Datos/Modelo Lógico Relacional/images/Untitled 15.png|Untitled]]

En este caso, en la nueva tabla solo nos bastará con las claves de las entidades con cardinalidad N para tener una llave primaria, debido a que para cada combinación de estas el docente será distinto, con lo que se pueden diferencias las tuplas (filas) unívocamente.

## Cardinalidad 1:1:N

![[Base de Datos/Modelo Lógico Relacional/images/Untitled 16.png|Untitled]]

En este caso también hacemos una cuarta tabla, pero solo tomaremos a una de las entidades con cardinalidad 1 y a la entidad con cardinalidad N como llaves primarias. La otra combinación queda como clave candidata.