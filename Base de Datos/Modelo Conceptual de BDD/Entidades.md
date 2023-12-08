### Conjunto de entidades

- Conjunto de ocurrencias o instancias de un determinado tipo de entidad en un estado determinado de la base de datos.

![[Base de Datos/Modelo Conceptual de BDD/images/Untitled 3.png|Untitled]]

# Restricción de unicidad

- Todo tipo de entidad debe tener un subconjunto del conjunto de [[Base de Datos/Modelo Conceptual de BDD/Atributos|atributos]] cuyos valores sean necesariamente distintos para cada una de las entidades en el conjunto de entidades.
- Dichos atributos se llaman ***atributos clave*** o ***identificadores únicos.***
- Si no los encontramos, debemos crear uno (id).
- Al ser distintos para cada entidad, los atributos clave permiten identificar unívocamente a las entidades.
- Los representaremos subrayados en el diagrama entidad relación.

![[Base de Datos/Modelo Conceptual de BDD/images/Untitled 1 2.png|Untitled]]

- El conjunto de atributos clave debe ser ***minimal,*** es decir, ningún subconjunto del mismo debe ser capaz de identificar unívocamente a las entidades.
- Aun así, es posible que exista más de un conjunto de atributos clave para un tipo de entidad.

# Entidades fuertes y débiles

- Cuando un tipo de entidad depende de otro para ser identificado, se dice que es un ***tipo de entidad débil***.
- La clave de una entidad débil se compone de la clave de su entidad identificadora, más algún/os atributos propios, que se denominan ***discriminantes*** y se indican con líneas punteadas.
- Un tipo de entidad débil siempre tiene participación total en el tipo de interrelación que la vincula con su tipo de entidad identificadora.

***Ejemplo:***

![[Base de Datos/Modelo Conceptual de BDD/images/Untitled 5.png|Untitled]]

En este caso tenemos hoteles y estos a su vez tienen muchas habitaciones. El número de una habitación se puede repetir en diferentes hoteles, por lo cual si solamente nos fijamos en el atributo de número este se va a repetir. Sin embargo, si tomamos como atributo clave ***{Hotel.nombre, Habitación.número}***, entonces estos sí serían únicos. Por lo que, al esta entidad depender de la entidad de Hotel, se la considera de tipo débil.

- Si es que modelamos una interrelación y esta tiene un atributo clave, entonces esto está mal. Lo que podemos hacer en esos casos es transformar esas interrelaciones en entidades débiles.