## Dominio

Es un conjunto de valores homogéneos

- $D_1$  = {Barcelona, Sevilla, Buenos Aires}
- $D_2$ = {Argentina, España, Chile}

## Producto Cartesiano:

$\text{A x B}$ se define como el conjunto de pares (a, b) que cumplen que $a \in A$  y $b \in B$.

- $D_1 XD_2 =$  {(Barcelona, Argentina), (Barcelona,
España), (Barcelona, Chile), (Sevilla, Argentina), (Sevilla, España), (Sevilla, Chile),(Buenos Aires, Argentina), (Buenos Aires, España), (Buenos Aires, Chile)}

## Relación

Es un subconjunto de un producto cartesiano

- R = {(Barcelona, España), (Sevilla, España), (Buenos
Aires, Argentina)}

## Esquema de relación

En el modelo relacional es un ***nombre de relación*** R junto con una lista de **atributos** asociados que se denota de la siguiente manera.

- $R(A_1, A_2,\dots,A_n)$
- Ej: Películas(nombre_película, año, nombre_director, cant_oscars).

Cada uno de los atributos $A_i$ de un esquema de relación está asociado a un ***dominio*** particular, $dom(A_i)$

- nombre_película → dom(nombre_pelicula) = string
- año → dom(año) = $\mathbb{N}^+$

Una relación R con esquema de ralación $R(A_1, A_2, \dots , A_n)$, estando los atributos $A_i$ asociados a los dominios $D_i = dom(A_i)$, es un subconjunto del producto cartesiano $D_1 XD_2X\dots D_n$.

- Dado el esquema de relación Películas(nombre_película, año, nombre_director, cant_oscars), se cumple que:
    - Películas ⊂ dom(nombre_pelicula) × dom(año ) ×
    dom(nombre_director) × dom(cant_oscars)

Un elemento de una relación se denomina ***tupla***.

- t = (Kill Bill, 2003, Quentin Tarantino, 0) es una tupla de Películas.
Lo denotamos como t $\in$ Películas.
- u = (Kill Bill, 2003, Quentin Tarantino, 3) no es una tupla de Películas porque los datos no son ciertos.
u  $\notin$ Películas.
- Podemos pensar a las relaciones como predicados y decir que Películas(Kill Bill, 2003, Quentin Tarantino, 3) = F
- Cardinalidad de una relación es la cantidad de tuplas que posee. Se simboliza ***n(R).***

## Tablas

Muchas veces las relaciones se representar a través de una tabla.

- Columnas → Atributos
- Filas → Tuplas

A veces se dice archivo en lugar de tabla, registro en lugar de fila y campo en lugar de columna.

# Restricciones

## Restricciones de Dominio

- Especifican que dado un atributo A de una relación R, el valor del atributo en una tupla *t* debe pertenecer al ***dom(A)***.
- Se puede permitir que algunos de los atributos tomen un valor nulo (NULL).
- Los atributos ***deben*** ser atómicos (no se permiten atributos compuestos o multivaluados).
- Dos tuplas distintas no pueden coincidir en los valores de todos sus atributos.
- Existe generalmente un subconjunto ***SK*** del conjunto de atributos $(A_1, A_2, \dots , A_3)$ de R que cumple la condición de que dadas dos tuplas $s, t \in R$, las mismas difieren en al menos uno de los atributos de ***SK.***
- Cuando un subconjunto ***SK*** cumple esta propiedad, diremos que ***SK*** es una ***superclave*** de SK.
- Cuando una superclave es también ***minimal*** (no admite un subconjunto de la misma que también sea superclave) entonces las llamaremos ***claves candidatas*** o simplemente ***claves***.
- De entre todas las claves candidatas elegiremos una como clave primaria de la relación (la indicamos subrayada).

### Restricción de integridad de entidad

La clave primaria de una relación no puede tomar un valor nulo

### Restricción de integridad referencial

Cuando un conjunto de atributos ***FK*** (foreign key, llave foránea) de una relación *R* hace referencia a la clave primaria de otra relación *S*, entonces para toda tupla de *R* debe existir una tupla de *S* cuya clave primaria sea igual al valor de *FK*, a menos que todos los atributos de *FK* sean nulos.

Esto en otras palabras nos dice que si un atributo en un esquema de relación es, en otro esquema de relación, una llave primaria, entonces cada instancia de la llave foránea DEBE estar en el esquema en donde esta es llave primaria.

Formalmente:

- Sean $R(A_1, A_2, \dots , A_r)$ y $S(B_1,B_2,\dots , B_s)$ dos esquemas de relación.
- $FK_{(A_1,A_2,\dots,A_r)}$ hace referencia a S, cuya clave primaria es $PK_{(B_1, B_2, \dots , B_s)}$.
- Entonces:

$$
\forall t \in R: t[FK] \neq NULL\implies\exists \ s\in S: s[PK] = t[FK]
$$

- FK se denomina clave foránea de S en R.
- Indicaremos las claves foráneas con un subrayado punteado.

# Operaciones

- ***Operaciones de consulta:***
    - No modifican ninguna relación exisstente
    - No violan ningún tipo de restricción
- ***Operaciones de inserción de tuplas***
    - Pueden violar restricciones de dominio, de unicidad y de integridad de entidad o referencial.
    - El SGDBD debería rechazar una inserción que viola algún tipo de restricción.
- ***Operaciones de eliminación***
    - Solo pueden violar restricciones de integridad referencial.
    - Cuando R referencia a S, y se intenta eliminar una tupla de S que es referenciada por alguna/s tupla/s en R.
    - Hay tres estrategias posibles: rechazar la eliminación, eliminar en cascada, o poner en NULL los atributos referenciales de las tuplas de R.
- ***Operaciones de modificación:***
    - Si se modifica una clave foránea, se debe verificar que sus nuevos valores referencies a una tupla existente de la relación referenciada, o bien sean todos nulos. De lo contrario se debería rechazar la operación.
    - Si se modifica una clave primaria puede violarse cualquiera de las restricciones de integridad y se combinan las situaciones indicadas para inserción y eliminación.

***Transacción →*** Conjunto ordenado de operaciones que o se ejecutan por completo o no se ejecutan. Puede que no se realice porque una de sus operaciones viola alguna restricción de integridad.