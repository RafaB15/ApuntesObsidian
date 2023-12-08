Decimos interrelación para no confundir las palabras en inglés.

Relación = Relation

Interrelación = Relationship

# Aridad

La ***aridad o grado*** de un tipo de interrelación es la cantidad de tipos de [[Base de Datos/Modelo Conceptual de BDD/Entidades|entidad]] que coparticipan del mismo.

Binarios → Participan dos entidades:

![[Base de Datos/Modelo Conceptual de BDD/images/Untitled 4.png|Untitled]]

# Restricciones Estructurales

## Cardinalidad

- Es la máxima cantidad de instancias de cada tipo de entidad que pueden relacionarse con una instancia concreta de los tipos de entidades restantes.
- Ejemplo:
    - Un futbolista solo puede haber nacido en un único país.
    - En un país pueden haber nacido muchos futbolistas.
- En interrelaciones binarias las cardinalidades posibles son:
    - 1:1 → Uno a uno
    - 1:N → Uno a muchos
    - N:1 → Muchos a uno
    - M:N → Muchos a muchos

![[Base de Datos/Modelo Conceptual de BDD/images/Untitled 1 3.png|Untitled]]

## Participación

- La participación es la mínima cantidad de instancias de cada tipo de entidad que deben relacionarse con una instancia concreta de los tipos de entidades restantes.
- Ejemplo:
    - Un futbolista ***debe*** haber nacido en algún país.
    - En un país ***puede*** no haber nacido ningún futbolista.
- Cuando requerimos que cada instancia de $E_1$ participe de alguna instancia de $r_1$ para poder subsistir, diremos que $E_1$ tiene ***participación total*** o ***dependencia existencial*** en $r_1$. En caso contrario diremos que tiene  **participación parcial**.
- Los indicaremos como (min, max) en el diagrama, en donde ***min*** denotará la participación y ***max*** denotará la cardinalidad del tipo de entidad en una interrelación dada.

![[Base de Datos/Modelo Conceptual de BDD/images/Untitled 2 2.png|Untitled]]

# Atributos

- Las interrelaciones también pueden tener atributos

![[Base de Datos/Modelo Conceptual de BDD/images/Untitled 3 1.png|Untitled]]

- En este ejemplo la fecha es un atributo tanto del alumno como de la asignatura, por lo que pasa a ser un atributo de su relación.
- En los tipos de interrelaciones también debemos identificar un conjunto de **atributos clave**.
- Solo pueden formar parte de los atributos clave de una interrelación los atributos clave de los tipos de entidad que participan en la misma.
- Recordar que la propiedad de los atributos clave es que si tomamos dos instancias distintas de un tipo de interrelación, los valores de su conjunto de atributos clave deben ser distintos. Podemos verlo como que las interrelaciones no van a tener un atributo clave en sí, pero si nos fijamos en los atributos clave de alguna de las entidades involucradas tendríamos que poder encontrar uno tal que para cada relación ese valor sea distinto.
    - Si la cardinalidad es 1:1 entonces cualquier atributo clave estará bien, porque en cada relación los valores serán distintos.
    - Si la cardinalidad es 1:N entonces elegimos el atributo clave de la entidad que tiene la N, pues la de 1 se repetirá en varias relaciones.
    - En el caso de tener una cardinalidad N:M tendremos que tomar como atributo clave de la interrelación a una tupla de un atributo clave de cada entidad que participa para que no se repita.

# Interrelaciones ternarias

- Son aquellas en donde participan 3 tipos de entidad distintos.

![[Base de Datos/Modelo Conceptual de BDD/images/Untitled 7.png|Untitled]]

- En este caso el conjunto de atributos clave es {Cantante.NroInscripción, Ronda.NroRonda, Jurado.Nombre}.
# Generalización y Especialización

- Nos permiten representar relaciones de tipo “es un” en el modelo de datos.

![[Base de Datos/Modelo Conceptual de BDD/images/Untitled 6.png|Untitled]]

![[Base de Datos/Modelo Conceptual de BDD/images/Untitled 1 4.png|Untitled]]

- Los subtipos de entidad son subclases del tipo de entidad padre.
- A través de la especialización se heredan atributos del tipo de entidad padre, al igual que los tipos de interrelación de los que la misma participa.
- Pero a su vez los tipos de entidad pueden tener atributos propios.
- Toda instancia de un subtipo de entidad debe corresponderse necesariamente con una y sólo una instancia del tipo de entidad padre.
- Resulta conveniente definir subtipos de entidad en nuestros modelos cuando:
    - Algunos atributos no se aplican a todas las instancias del tipo de entidad padre.
    - Un tipo de interrelación no se aplica a todas las instancias del tipo de entidad padre.

## Propiedades

### Superposición

Los subtipos de entidad pueden ser ***disjuntos*** o ***superpuestos***. En caso de ser superpuestos, una instancia del tipo de entidad padre puede corresponderse con instancias de varios subtipos de entidad.

### Completitud

Los subtipos de entidad pueden cubrir a todo el tipo de entidad padre (***total***), o no (***parcial***). En caso de no cubrirlo, puede ocurrir que algunas instancias de tipo de entidad padre no se corresponda con ningún subtipo de entidad.

En el ejemplo anteriror, la especialización es superpuesta (una persona puede ser alumno y docente a la vez) y total (toda persona registrada debe ser alumno o docente). 

# Unión

- En la unión también tenemos un tipo de entidad padre y distintos subtipos de entidad.
- Pero ahora el tipo de entidad padre es subclase de los subtipos de entidad (que son la superclase).
- Esto implicará que los identificadores estarán en los subtipos de entidad, mientras que el tipo de entidad padre incorporará nuevos atributos.
- Las instancias del tipo de entidad padre deben corresponderse con ***a lo sumo una*** instancia de los subtipos de entidad.

***Ejemplo:*** Un banco tiene como clientes tanto a personas físicas como a personas jurídicas radicadas en argentina

![[Base de Datos/Modelo Conceptual de BDD/images/Untitled 2 3.png|Untitled]]

El cliente ***es una*** persona física o bien ***es una*** persona jurídica. Pero ***no*** necesariamente una persona física debe ser un cliente del banco.