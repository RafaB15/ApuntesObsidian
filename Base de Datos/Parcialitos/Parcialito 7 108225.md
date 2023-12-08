# Ejercicio 1

## Enunciado

Dado el siguiente esquema sobre profesores de una facultad:
- profesores(legajo, nombre, apellido, genero, titulo) 

Se pide: 
### Parte 1

Analice cuál es el método de acceso más eficiente para resolver la siguiente consulta y estime su costo (en bloques accedidos):
$$\sigma_{titulo=LICENCIADO\  \wedge \ genero=M}(profesores)$$
### Parte 2 

Estime la cantidad de tuplas devueltas por dicha selección

Información que se posee: 
- $n(profesores) = 500$ y $F(profesores) = 25$. 
- $V(titulo, profesores) = 10$ y $V(genero, profesores) = 2$. 
- La tabla profesores tiene un índice llamado **prtit** por título con $Height(prtit) = 2$. Este índice no es de clustering. 
- Los valores de las columnas titulo y genero se almacenan siempre en mayúsculas.

## Resolución

### Parte 1

Podemos apreciar que, de los dos atributos pertenecientes a la condición de selección, el atributo **título** tiene un índice, llamado **prtit**, con lo cual podemos aprovechar esto para hacer la selección.

El método cuando tenemos un atributo con índice y otro sin índice es hacer la selección únicamente por el atributo con índice y cuando recuperamos la tupla evaluar también la segunda condición, por lo que el costo de traer los bloques de disco a memoria será únicamente el de la consulta que tiene índice.

Debido a que título no es una clave primario y se nos indica que no es de clustering, entonces la única opción que queda es que es un índice secundario.

El costo de hacer una búsqueda con índice secundario es
$$P = profesores$$
$$cost(\sigma) = Height(I(titulo, P)) + \frac{n(P)}{V(titulo,P)}$$
Sabemos que:

- $I(titulo, P) = prtit$
- $Height(prtit) = 2$
- $n(P)$ = 500
- $V(titulo, P)$ = 10

Con lo que nuestra ecuación quedaría:
$$cost(\sigma) = 2 + \frac{500}{10} = 52$$

Por lo que el costo estimado de bloques accedidos es 52.

### Parte 2

La relación profesores tiene un total de 500 tuplas. Al hacer una selección este número se va a reducir. 
Con una condición simple, la nueva cantidad de tuplas se **definiría** por la siguiente fórmula:

$$n(\sigma_{cond} (P)) = \frac{n(P)}{V(titulo , P)}$$

Dividimos la cantidad de tuplas por la varianza debido a que estamos igualando a uno de los valores del atributo.

Sin embargo, en nuestro caso tenemos una condición más compleja, que involucra a otro atributo, lo cual será un filtro más, que hará que tengamos todavía menos tuplas. 

Como vamos a volver a filtrar el resultado de filtrar por el primer atributo, lo dividimos de nuevo.

$$\displaystyle \large n(\sigma_{cond} (P)) = \frac{\frac{n(P)}{V(titulo , P)}}{V(genero, P)}$$
$$\displaystyle \large n(\sigma_{cond} (P)) = \frac{\frac{500}{10}}{2} = 25$$

Con lo cual, se espera que el resultado de la consulta de como resultado 25 tuplas.

# Ejercicio 2

## Enunciado

Dado el siguiente esquema que registra cuando un usuario le da “Me gusta” a una publicación:

- megusta(id usuario, id publicación, fecha_hora)

Se busca encontrar pares de usuario a los que les guste una misma publicación. Se pide:

### Parte 1

Analice cuál es el método de acceso más eficiente para resolver la siguiente consulta y estima su costo (en bloques accedidos):

$$\displaystyle \large megusta \bowtie_{id\_usuario \not= id\_usuario \wedge id\_publicación = id\_publicación} megusta$$

### Parte 2

Estime la cantidad de tuplas devueltas por dicha selección.

Información que se posee:

- $n(megusta) = 100,000,000 = 10^8$
- $F(megusta) = 1000 = 10^3$
- $V(id\_usuario, megusta) = 50000 = 5 * 10^4$ 
- $V(id\_publicación, megusta) =10,000,000 = 10^7$ 
- No se cuenta con índices 
- Se dispone de $M = 1,001$ bloques de memoria disponibles.

## Resolución

### Parte 1

Queremos hacer una junta de una tabla consigo misma para emparejar todas las tupas con distinto id de usuario, pero igual id de publicación.

$$megusta = G$$

Hay diferentes métodos que podemos utilizar para hacer la junta, algunos de los cuales se beneficiarían si pudiéramos tener más de dos bloques en memoria a la vez. Hay que tener en cuenta que la cantidad de bloques que tiene la relación megusta la podemos obtener de la siguiente manera:

$$F(G) = \frac{n(G)}{B(G)} \implies B(G) = \frac{n(G)}{F(G)} = \frac{10^8}{10^3} = 10^5$$
Con lo cual la memoria que sería requerida para tener una tabla en memoria sería $10^5$ bloques.

Usando **loops anidados** por bloque, el costo utilizando únicamente dos bloques de memoria a la vez sería de:

$$cost(G\bowtie G) = B(G) \cdot (1 + B(G)) = 10^5 + 10^{10}$$
Podríamos mejorar este resultado si pudiéramos meter una tabla entera en memoria, sin embargo eso requeriría de $10^5 + 1$ bloques, y nosotros disponemos de $10^3 + 1$.

Usando **sort-merge**, tendremos que ordenar la tabla (la ordenamos en base a id_publicación, pues es la igualdad, con lo que nos servirá recorrer en orden para encontrar coincidencias) y volverla a guardar en memoria, lo cual tendrá un costo de $2 \cdot B(G) \cdot [log_{M -1}(B(G))]$. A esto se le suma el costo de recorrer la tabla dos veces para compararla, siendo el costo final de la operación:

$$cost(G \bowtie G) = 2 \cdot B(G) + 2 \cdot B(G) \cdot [log_{M -1}(B(G))]$$ 
$$cost(G \bowtie G) = 2 \cdot 10^5 + 2 \cdot 10^5 \cdot [log_{1000}10^5] = 2\cdot 10^5 + 2 \cdot 10^5 \cdot \frac{5}{3} \approx 6 \cdot 10^5 $$ 
Usando el método de **junta hash**, el costo para particionar la tabla, dado que se tienen que leer todos los bloques y reescribir en otro orden todos los datos, $2 \cdot B(G)$. El costo para combinar las tablas es de $B(G) + B(G)$, con lo cual, el costo total para este método es de:

$$cost(G \bowtie G) = 4 \cdot B(G) = 4 \cdot 10^5$$


Vemos que de todos los métodos vistos, el más eficiente sería la junta hash.

### Parte 2

La formula general para estimar la cardinalidad de la junta entre dos tablas *R* y *S* que se juntan en base a la igualdad de un valor B es:

$$n(R*S) = \frac{n(R)\cdot n(S)}{max(V(R,B), V(S,B))}$$

En nuestro caso, si tenemos en cuenta solo la condición de igualdad del id de publicación la cardinalidad sería la siguiente

$$n(G*G) = \frac{n(G)^2}{V(G, id\_publicación)} = \frac{10^{16}}{10^7}=10^9$$

Entonces, nuestra estimación de cuantas tuplas en la junta tendrán igual id de publicación es $10^9$. Sin embargo, a estas tuplas habrá que sacarle las que tengan igual id de usuario. 

Pensándolo un poco, cada tupla de la tabla original va a tener un id_usuario y un id_publicación, por lo que cuando se haga la junta solo por igual id_publicación, todas las tuplas serán incluidas consigo mismas al tener el mismo id. Entonces sabemos que dentro de nuestra junta va a haber tantas tuplas con id_usuario iguales como tuplas en la tabla original. Con lo cual, nuestra nueva estimación de cardinalidad esperada sería.

$$n(G*G) = 10^9 - n(G) = 10^9 - 10^8 = 10^8 (10 - 1) = 9\cdot 10^8$$ 
Con esto, nuestra nueva cardinalidad esperada es $9\cdot 10^{8}$.