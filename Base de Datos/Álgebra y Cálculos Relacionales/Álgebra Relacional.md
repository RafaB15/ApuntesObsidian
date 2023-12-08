- Es un lenguaje procedural.
- Provee un marco formal de operaciones para el modelo relacional.
- Se emplea como base para optimizar la ejecución de consultas.
- Especifica los procedimientos de consulta de datos a partir de un conjunto de **operaciones**.
### Operación
En el contexto del modelo relacional, es una función cuyos operandos son una o más relaciones, y cuyo resultado es también una relación.
$$O: R_1 \times R_2 \times \dots \times R_n \to S$$
**Aridad**: Cantidad de operandos que toma una operación.
**Expresión**: Combinación de operaciones del álgebra relacional.
# Operaciones Básicas
## Selección 
El operador de **selección** $\sigma$ es un operador unario.
$$\displaystyle \huge \sigma_{cond}: R \to S$$
Dada una relación $R(A_1, A_2, \dots , A_n)$ y una condición que se aplica a cada tupla de R, $\sigma_{cond}(R)$ selecciona aquellas tuplas de R para las cuales la condición es verdadera.
![[Ejemplo Selección.png]]
Utilizamos operaciones atómicas de la forma:
- $A_{i} \ \odot \ A_j$
- $A_{i} \ \odot \ c$, con $c \in dom(A_i)$
En donde $\odot$ debe ser un operador de comparación
- $=, \ne$
- $>,\ge , <, \le$ (para atributos con dominios ordenados)

Una condición se construye combinando condiciones atómicas con los operadores lógicos and $\wedge$ , or $\vee$ y not 
$$\displaystyle \huge\sigma_{(local\_club='Barcelona')\wedge (birth\_year<2000)}(Players)$$
## Proyección
El operador de **proyección** $\pi$ es un operador unario.
$$\displaystyle \huge \pi_{L}: R \to S$$
Dada una relación $R(A_1, A_2, \dots , A_n)$ y una lista de atributos $L = (L_1, L_2, \dots , L_n)$, con $L_i \in (A_1, A_2, \dots, A_n)$, $\pi_L(R)$ devuelve una relación cuyas tuplas representan los posibles valores de los atributos de $L$ en $R$.
Podemos pensar que lo que hace es proyectar cada tupla de *R* a un espacio de menor dimensión en que sólo se conservan los atributos que están en L.
![[Ejemplo Poryección.png]]
El orden de los atributos en la realción resultado es el mismo orden en que figura en *L*.
El operador de proyección siempre remueve *tuplas duplicadas*, ya que su resultado debe ser también una relación válida.
## Asignación
Se denota con una flecha $\leftarrow$ y se usa para darle un nombre a las nuevas relaciones que obtengamos.
$$
\displaystyle \huge
\begin{aligned}
Temp & \leftarrow \sigma_{group  = 'G'}(NationalTeams) \\ 
Selecciónes_GrupoD &\leftarrow \pi_{name}(Temp)
\end{aligned}
$$
## Redenominación
El operador de redenominación $\rho$  permite modificar los nombres de los atributos de una relación y/o el de la relación misma.
Dada una relación  $R(A_1, A_2, \dots , A_n)$, un nuevo nombre de relación *S* y una lista de *n* nombres de atributo $(B_1, B_2, \dots , B_n)$, $\rho_{S(B_1,B_2, \dots, B_n)}(R)$ produce una relación de nombre S y atributos $(B_1, B_2, \dots, B_b)$ cuyas tuplas coinciden con las tuplas de *R*.
$\rho_S(R)$ solo cambia el nombre de la relación *R* por *S*.
## Unión

Dadas dos relaciones $R(A_1, A_2, \dots , A_n)$ y $S(B_1, B_2, \dots , B_n)$, la unión $R \cup S$ es una relación que contiene a todas las tuplas de *R* y de *S*.
Requiere **[[Compatibilidad de Tipos|compatibilidad de tipos]]*.
Por convención, en la relación resultado el listado de atributos coincide con el de $R: (A_1, A_2, \dots, A_n)$.
![[Ejemplo Unión.png]]
## Intersección

Dadas dos relaciones $R(A_1, A_2, \dots , A_n)$ y $S(B_1, B_2, \dots , B_n)$, la intersección $R \cap S$ es una relación que conserva las tuplas que se encuentran presentes tanto en *R* como en *S*.
*R* y *S* deben tener el mismo grado. Requiere [[Compatibilidad de Tipos|compatibilidad de tipos]].
![[Ejemplo Intersección.png]]
## Diferencia

Dadas dos relaciones $R(A_1, A_2, \dots , A_n)$ y $S(A_1, A_2, \dots , A_n)$, la diferencia $R - S$ conserva soloa quellas tuplas de *R* que no pertenecen a *S*.
R y S deben tener el mimo grado. Requiere [[Compatibilidad de Tipos|compatibilidad de tipos]].
![[Ejemplo Diferencia.png]]
## Producto Cartesiano

Dadas dos relaciones $R(A_1, A_2, \dots , A_n)$ y $S(B_1, B_2, \dots , B_n)$, el producto cartesiano $R \times S$ produce una nueva realción *T* cuyas tuplas son todas aquellas de la forma $(t_1, t_2, \dots, t_n, t_{n + 1}, t_{n+2}, \dots, t_{n+m})$ con  $(t_1, t_2, \dots, t_n) \in R$ y $(t_{n + 1}, t_{n+2}, \dots, t_{n+m}) \in S$.
El esquema de la nueva relación *T* es $(A_1, A_2, \dots, A_n, B_1, B_2, \dots, B_n)$. Si el nombre de alguno de los atributos de las relaciones coincide entonces las ponemos como $R.A_i$ y $S.B_j$. Si estamos calculando $R \times R$ llamaremos a los atributos $R1.A_j$ y $R_2.A_j$.
No requiere [[Compatibilidad de Tipos|compatibilidad de tipos]].
![[Ejemplo Producto Cartesiano.png]]
## Árbol de Consulta

Para cada expresión del álgebra relacional se puede construir un árbol de consulta que representa el orden de ejecución.
## Junta

*Junta = Join*
La operación de junta combina un producto cartesiano con una selección.
Dadas dos relaciones $R(A_1, A_2, \dots , A_n)$ y $S(B_1, B_2, \dots , B_n)$ y una condición, la junta $R\bowtie_{cond}S$ selecciona del producto cartesiano $R \times S$ las tuplas que cumplen la condición.

No se admite cualquier tipo de condición de selección, sino sólo la conjunción de operaciones atómicas que incluyen columnas de ambas relaciones, es decir, de la forma:
$$A_i \odot B_j$$En donde $\odot$ debe ser un operador de comparación ($=, \ne, >, \ge, <, \le$).
Una condición se construye entones combinando operaciones atómicas con el operados lógico and ($\wedge$).

**Junta Natural**: No se especifican condiciones, sino que se espera que en ambas tablas haya un atributo de nombre igual y se va a hacer la junta en base a los que coincidan. Se representa con $S*R=T$

## División

- Partimos de una relación $R(A_1, A_2, \dots, A_n)$ y una relación $S(B_1, B_2, \dots, B_m)$ cuyos atributos están incluídos en los de *R*. 
- Llamamos $A = {A_1, A_2, \dots, A_n}$ y $B = {B_1, B_2, \dots, B_m}$. Entonces $B \subset A$.
- Llamamos $Y = A- B$.
Definimos entonces la **división** $R \div S$ como la relación $T(Y)$ que contienen todas las tuplas *t* que cumplen que:
- *t* pertenece a $\pi_Y(R)$
- Para cada tupla $t_S \in S$ existe una tupla $t_R\in R$ tal que $t_R[Y]=t$ y $t_R[B] = t_S$.
**Propiedad:** T es la relación de mayor cardinalidad posible contenida en $\pi_Y(R)$ y que cumple que $T * S \subset R$.
![[Ejemplo División.png]]
En una división, si las columnas que no están dividiendo son dis
## Junta Externa
*Son como los joins en SQL y Pandas*