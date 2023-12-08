- Dada una [[Base de Datos/Modelo Lógico Relacional/Modelo Relacional#Relación|relación]] $R(\overline A)$, una dependencia funcional $X \to Y$, con $X,Y \subset \overline A$ es una restricción sobre las posibles tuplas de *R* que implica que dos tuplas con igual valor del conjunto de [[Base de Datos/Modelo Conceptual de BDD/Atributos|atributos]] *X* deben también tener igual valor del conjunto de atributos *Y*.
- Esto es: 
$$\displaystyle \large \forall s,t \in R: s[X] = t[X] \to s[Y] = t[Y]$$
- La dependencia funcional $X \to Y$ implica que hay una relación funcional entre los valores de *X* y los de *Y* dentro de la base de datos.
- Las dependencias funcionales se definen a partir de la semántica de los datos. No es posible inferirlas viendo los datos.
	- Si vemos una tabla, podemos decir cuales dependencias no rigen, por encontrar un caso en el que no se cumpla la condición. Pero no podemos garantizar que una dependencia rige.
	- Para entender cuales dependencias funcionales rigen, tenemos que saber qué representan los datos.
- A las dependencias se les puede agregar cosas que no sirven a ambos lados. La clausura es lo que expresan. 
- Se intenta encontrar un conjunto de dependencias que sea minimal y nos de toda la clausura (información).
- Las claves primarios son dependencias funcionales de ellas al resto de los atributos incluyéndose a sí mismos.
- Solo hay un valor en Y para cada valor de X, pero un mismo valor de Y puede corresponder a varios valores en X.

# Tipos

## Trivial

Cuando $Y \subset X$ decimos que $X\to Y$ es **trivial**.

## Parcial

Una dependencia $X \to Y$ es **parcial** cuando existe un subconjunto propio $A \subset X$, $A \not= X$ para el cual $A \to Y$.
Podría decirse que en *X* sobran atributos, y que con unos cuantos nos basta para identificar *Y*.

{asignatura, profesor} -> {asignatura} -> {departamento}
## Total

Una dependencia $X \to Y$ es **total** cuando no es parcial. 

## Transitiva

Una dependencia funcional $X\to Y$ es transitiva cuando existe un conjunto de atributos *Z* que satisface dependencias $X \to Z$ y $Z \to Y$, siendo $Z \to Y$ no trivial, $X \to Y$ no trivial y $Z \not \to X$ 

Observación: Toda dependencia funcional parcial no trivial es transitiva.

# Inferencia de DF

## Axiomas de Armstrong

### Axioma de reflexividad

$$Y \subset X \implies X \to Y$$
### Axioma de aumento

$$\forall W:X\to Y \implies XW \to YW$$

### Axioma de transitividad

$$X \to Y \wedge Y \to Z \implies X \to Z$$
- Estos axiomas pueden ser probados a partir de la definición de dependencia funcional.
- Los tres axiomas en conjunto son completos. Toda *df* que se puede inferir de *F* se puede inferir a través de los axiomas de Armstrong.
- La notación $F \vDash X \to Y$ indica que la dependencia funcional $X \to Y$ puede inferirse a partir del conjunto de dependencias funcionales *F*.

## Reglas

## Regla de unión:

$$X \to Y \wedge X \to Z \implies X \to YZ$$

### Regla de pseudotransitividad

$$\forall W : X \to Y \wedge YW \to Z \implies XW \to Z$$

### Regla de descomposición:

$$X \to YZ \implies X \to Y \wedge X \to Z$$

# Clausura

- Partimos de una relación $R(A_1, A_2, \dots, A_n)$.
- Dado un conjunto de dependencias funcionales *F*, la **clausura de** $F(F^+)$ es el conjunto de todas las dependencias funcionales que pueden **inferirse** de *F*.
$$F^+ = \{(X \to Y) | F \vDash (X \to Y)\}$$
- Dado un conjunto de atributos *X* y un conjunto de dependencias *F*, la **clausura de *X* con respecto a** $F(X^+_F)$ es el conjunto de todos los atributos $A_i$ tales que la dependencia funcional $X\to A_i$ se infiere del conjunto de dependencias *F*. 
$$X^+_F = \{A_i | F \vDash (X \to A_i)\}$$
- Las clausuras de conjuntos de atributos $X_F^+$ son una forma ordenada de construir $F^+$.
- Esta clausura nos permite dar otra definición de clave candidata: Dado un esquema de relación $R(A_1, A_2, \dots, A_n)$ y un conjunto de dependencias funcionales *F*, *CK* es clave candidata de *R* si y sólo si $CK_F^+ = A_1A_2\dots A_n$ y ningpun subconjunto propio cumple con esa propiedad.

# Forma canónica

Para que un conjunto de dependencias funcionales *F* esté en forma canónica, entonces se debe descomponer las dependencias funcionales que tienen a su derecha más de un valor en varias dependencias funcionales.

$$X \to Y \text{ pasa a ser } X \to A_i \text{ con } A_i$$

# Cobertura y equivalencia

- Dados dos conjuntos de dependencias funcionales *F* y *G*, decimos que el conjunto *F* **cubre** a *G* cuando toda dependencia funcional $X \to Y \in G$ puede ser inferida a partir de *F*. Es decir

$$\forall (X \to Y) \in G: F \vDash X \to Y$$
- Dos conjuntos de dependencias funcionales *F* y *G* son **equivalentes** cuando cada uno de ellos es **cubierto** por el otro. En otras palabras, *F* y *G* son equivalentes cuando sus clausuras coinciden: $F^+ = G^+$. Lo simbolizaremos con $F \equiv G$. 

# Cubrimiento minimal

- Dado un conjunto de dependencias *F*, nos interesará encontrar un conjunto equivalente *G* que cumpla ciertas propiedades de minimalidad. En particular, nos interesa que:
	- No haya atributos innecesarios del lado izquierdo:
	$$\forall (X \to Y) \in G: \not \exists (Z \to Y) \in G,Z \subset X,Z \not = X$$
	- No haya dependencias redundantes
	$$\not \exists (X \to Y) \in G: G - \{X \to Y\} \equiv G$$
- A todo conjunto de dependencias funcionales *G* que es equivalente a *F* y cumple estas dos propiedades lo denominamos **cubrimiento minimal de $F$**.

# Proyección de DF

- Al [[Base de Datos/Diseño Relacional/Descomposición|descomponer]] una relación *R* con un conjunto de dependencias funcionales *F* en $D = (R_1(Z_1), R_2(Z_2), \dots, R_n(Z_n))$, es necesario saber qué dependencias funcionales se preservan.
- Las dependencias que se preservan son las que surgen de la proyección de *F* sobre los atributos $Z_i$ de cada uno de las $R_i(Z_i)$.
- La proyección de un conjunto de dependencias funcionales *F* sobre un conjunto de atributos *Z*, $F_Z$, se define como:
$$F_Z^+=\{X\to Y\in F^+ | X \cup Y \subset Z\}$$
- Las *df* preservadas en la descomposición son entonces 
$$F_D^+ = (F_{Z_1} \cup F_{Z_2} \cup \dots \cup F_{Z_n})^+$$
# Algoritmos

## Conseguir clausura de atributos X con respecto a F

**Input:** Un conjunto de dependencias funcionales *F* de una relación universal *R*, un conjunto de atributos X.
**Output**:  La clausura de *X* con respecto a *F*, $X_F^+$ 
**Algoritmo**:

![[Base de Datos/Diseño Relacional/images/Algoritmo clausura atributo.png]]
En este algoritmo básicamente vamos iterando sobre todas las *df* y viendo cuales se pueden inferir de *X*, luego nos fijamos en cuales se pueden inferir de las inferidas de *X* y así hasta que no se nos agregue ninguna nueva.

## Conseguir cubrimiento minimal de F

- El algoritmo de cubrimiento minimal tiene 3 grandes pasos:
	1. Pasar las dependencias funcionales a forma canónica.
	2. Eliminar los atributos innecesarios del lado izquierdo de cada dependencia funcional $X \to A_i$.
	3. Eliminar las dependencias funcionales redundantes.
 
**Input:** Un conjunto de dependencias funcionales *F*.
**Output:** Un cubrimiento minimal de $F, F_{min}$.

![[Base de Datos/Diseño Relacional/images/Algoritmo de cubrimiento mínimo.png]]

Para hacerlo a mano conviene conseguir las clausuras de cada atributo de la relación universal para ayudarse a ver qué implica quitar o agregar uno.

## Conseguir Claves Candidatas

Dada una relación $R(A_1, A_2, \dots, A_n)$, podemos encontrar las claves candidatas a partir de un conjunto de dependencias funcionales *F*.

1. Calcular el cubrimiento minimal del conjunto de dependencias funcionales *F*. Inicializar el conjunto de atributos de cálculo $C_a = \{A_1, A_2, \dots, A_n\}$.
2. Hallar los atributos independientes del cálculo, $A_{indep}$, que son aquellos que no están presentes en ninguna dependencia funcional. Eliminarlos del conjunto de atributos de cálculo: $C_a = C_a - A_{indep}$.
3. Hallar los conjunto de términos equivalentes, $A_{equiv}$, que son aquellos pares $(X,Y)$ de términos que cumplen que $X \to Y$ y $Y\to X$ (con $X \cap Y = \emptyset$). De cada conjunto de términos equivalentes dejar sólo uno, y eliminar los restantes de $C_a$. Calcular la proyección de $F_{min}$ en $C_a, F_c$. (Las dependencias que tenían al equivalente que quitamos las reescribimos si es necesario).
4. Construir una clave tentativa $K_{tent}$ con todos los elementos que sean sólo implicantes en $F_C$ (es decir, estén sólo en la parte izquierda). Si $K^+_{tent} = C_a$ entonces $K_{tent}$ es clave.
5. Si $K_{tent}$ no resultó clave, entonces se comienzan a agregar otros atributos que sean implicantes, pero que puedan ser implicados también. Se agregan alternativamente a $K_{tent}$ todos los posibles subconjuntos de 1 atributo, luego aquellos de 2 atributos, etc, del conjunto $C_a - K_{tent}^+$. Con cada uno de ellos se verifica si $K_{tent}$ es clave de $C_a$ calculando la clausura. Al hacer crecer los subconjuntos se deben obviar aquellos que resultaron ser clave de $C_a$, ya que no van a ser minimales.
6. Por cada $K_{tent}$ encontrado como clave de $C_a$ se unen los atributos independientes, $A_{indep}$ para obtener *K*, y se agrega *K* al resultado *CKs*.
7. Se calculan otras claves *K* con otros de los términos equivalentes encontrados en el paso 3, y se agregan todas al resultado,  *CKs*.
