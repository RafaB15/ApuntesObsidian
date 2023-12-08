- **Relación Universal**: Una relación $R(A_1, A_2, \dots , A_n)$ que engloba todos los atributos del mundo real que nuestro modelo lógico representa.

- Dada una relación universal $R(A_1, A_2, \dots , A_n)$ y un conjunto de [[Base de Datos/Diseño Relacional/Dependencia Funcional|dependencias funcionales]] *F* definidas sobre ella, decimos que un conjunto de relaciones $\{R_1(B_{11}, B_{12}, \dots , B_{1n_1})\dots , R_m(B_{m1}, B_{m2}, \dots B_{mn_m})\}$ es una descomposición de *R* cuando todos los atributos de la relación *R* se conservan. Es decir
$$\displaystyle \huge \bigcup_{i = 1}^{n}A_i = \bigcup_{i=1}^{m}\bigcup_{j=1}^{n_j}B_{ij}$$
- Propiedades
	- Preservación de información
	- Preservación de dependencias funcionales.
- Si una descomposición cumple que para toda instancia posible de *R*, la junta de las proyecciones sobre los $R_i$ permite recuperar la misma instancia de relación, entonces decimos que la descomposición preserva la información.
	- Esta implica que dada una relación *R* y una descomposición de *R* en $D = (R_1(Z_1), R_2(Z_2), \dots, R_n(Z_n))$, toda instancia *r* de *R* puede recuperarse como $$\displaystyle \large r = \pi_{Z_1}(r) *\pi_{Z_2}(r) * \dots * \pi_{Z_n}(r)$$
- Diremos que la descomposición preserva las dependencias funcionales cuando toda dependencia funcional $X\to Y$  en *R* puede inferirse a partir de dependencias funcionales definidas en los $R_i$.
- Si una descomposición cumple con ambas propiedades se la conoce como descomposición equivalente de R.

# Algoritmo para verificar preservación de información

Para verificar que una descomposición de una relación *R* preserva la información podemos utilizar el algoritmo de chase. 

Si tenemos la relación 

- $R(ABCD), F = \{A\to C, B \to D, AB \to CD\}$:
	- $R_1(AC)$
	- $R_2(BD)$
	- $R_3(AB)$

Primero armamos una tabla que tenga tantas filas como relaciones y tantas columnas como atributos.

El algoritmo parte de una hipotética tupla $(a_1, a_2, a_3, a_4)$ de la junta $r_1 \bowtie r_2 \bowtie r_3$ que se proyecta a cada una de las $r_i$. si una relación $r_i$ contiene un atributo $A_j$, entonces en la posición $(i,j)$ de la tabla escribimos el valor abstracto $a_j$. Caso contrario ponemos un valor $b_{i,j}$

![[Primera tabla chase.png]]

Por la dependencia $A \to C$, como en R1 están A y C y en R3 solo A, podemos reemplazar $b_{33}$ por $a_3$ porque la podemos obtener. Lo mismo con B y D
![[Pasted image 20231004171400.png]]

Como nos queda una fila entera con valores de a, significa que la descomposición preserva la información.

Podemos usar las *a* en cada fila como si ya tuvieramos el valor en esa fila.

Basicamente nos damos cuenta que si se cumple que $B \to D$, entonces en la tabla, si vemos que hay alguna *a* en la columna B que tenga una *a* en la columna D, entonces como igual a en B significa igual valor en D, ponemos una a también ahí.