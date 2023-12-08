- Es un lenguaje declarativo, de más alto nivel que el álgebra relacional.
- Al no ser procedural, no especifica un orden de operaciones a realizar.
- Está basado en la lógica de predicados.
- Presenta dos variantes:
	- El cálculo relacional de tuplas.
	- El cálculo relacional de dominios.
- El lenguaje SQL está inspirado en el cálculo relacional de tuplas.

# Definiciones
## Proposiciones

Son hechos siendo declarados que tienen cierta estructura:
- Rafael Nadal ganó el torneo de Roland Garros en 2009.
- Gabriela Sabatini ganó el Abierto de Estados Unidos en 1990.
## Predicado

Un conjunto de proposiciones que tienen la misma estructura puede tipificarse a través de un predicado.
- \[tenista] ganó \[torneo] en \[año]

Un predicado es una función cuyo resultado es un valor de verdad: Verdadero o Falso
- TenistaCampeón(nombre_tenista, nombre_torneo, año)
- Entonces
	- TenistaCampeón(Rafael Nadal, Roland Garros, 2011) = V
	- TenistaCampeón(Juan Martín del Potro, Roland Garros, 2011) = F

En el cálculo relacional, los esquemas de relación pueden pensarse como predicados.
- Las bases de datos sólo almacenan proposiciones verdaderas. 
- Cada tupla t de una relación R predica que R(t) = V.

# Lógica de Predicados de Primer Orden

- La lógica de predicados de primer orden se basa en: 
	- Predicados: Son funciones de una o más variables cuyo resultado es un valor de verdad (V ó F). 
		- Ejemplo: p(m, n). 
	- Operaciones entre predicados. 
		- $\wedge, \vee, \neg, \to$ 
		- Combinando los predicados con operaciones se obtienen predicados más complejos 
		- Ejemplo: $(p(m,n) \wedge \neg q(m)) \vee q(n)$. 
	- Cuantificadores de variables. 
		- Cuantificador universal: $(\forall m)q(m)$. Es verdadero si para cualquier valor de m el predicado q(m) es verdadero. 
		- Cuantificador existencial: $(\exists m)q(m)$. Es verdadero si existe al menos un valor de m para el cual el predicado q(m) es verdadero.

# Cálculo relacional de Tuplas

- En el cálculo relacional de tuplas las variables representan tuplas.
- Un **predicado simple** es una función de una tupla o de atriutos de tuplas, cuyo resultado es un valor de verdad (V ó F). Se admiten como predicados simples:
	- *R(t)*, en donde *R* es una relación. 
		- Dará true si es que *t* pertenece a *R*.
	- $t_1 . A_i \odot t_2 . A_j$ 
	- $t_1 . A_i \odot c$, con $c \in dom(A_i)$ 
	- En donde $\odot$ debe ser un operador de comparación 
		- $=, \ne$
		- $>,\ge , <, \le$ (para atributos con dominios ordenados).
- Las operaciones entre predicados admitidas son  $\wedge, \vee, \neg$.
- Ejemplo:
	- Liste los nombres de los jugadores nacidos antes de 1980.
	- $\{p.name|Players(p) \wedge p.birth\_year <1980\}$
		- A la izquierda de la barra ponemos las partes de la tupla que queremos mostrar, a la derecha las condiciones de las tuplas para ser seleccionadas.

## Cuantificadores

### Cuantificador universal 
$$\displaystyle \huge (\forall m)q(m)$$
Es verdadero si para cualquier valor de m el predicado q(m) es verdadero. 

### Cuantificador existencial 
$$\displaystyle \huge (\exists m)q(m)$$
Es verdadero si existe al menos un valor de m para el cual el predicado q(m) es verdadero.

Ejemplo:
- Listado de los nombres de los jugadores que hicieron goles:
- $\{p.name|Players(p) \wedge (\exists s)(Scores(s) \wedge s.player\_id = p.id)\}$

Cabe resaltar que las variables que fueron cuantificadas no pueden aparecer seleccionadas en el lafo izquierdo de la barra, y toda variable que aparece sólo en el lado derecho debe estar cuantificada.
- **Variables Ligadas** $\to$ Variables que fueron cuantificadas.
- **Variables Libres** $\to$ Variables que no fueron cuantificadas.

**Expresión segura** $\to$ Es una expresión que garantiza formalmente que producirá una cantidad finita de tuplas.

- ${p_1.nombre|(\exists p_2)(Personas(p_2) \wedge p_2.edad = p_1.edad)}$ 
	- Expresión no segura 
	- Probablemente queríamos ${p_1.nombre|Personas(p_1) \wedge (\exists p_2)(Personas(p_2) \wedge p_2.edad = p_1.edad)}$

## Relación entre los cuantificadores

$(\exists y)(f(y)) \iff (\not \forall y)(\neg f(y))$
$(\not \forall y)(f(y)) \iff (\not \exists y)(\neg f(y))$ 

# Cálculo relacional de Dominios

- En el cálculo relacional de dominios las variables representan dominios, es decir que hacen referencia a los atributos. 
- Un **predicado simple** es una función de un conjunto de dominios, cuyo resultado es un valor de verdad (V ó F). Se admiten como predicados simples:
	- $R(x_1, x_2, ..., x_n)$, en donde $R(A_1, A_2, \dots, A_n)$ es una relación 
	- $x_i \odot x_j$  
	- $x_i \odot c$, con $c \in dom(A_i)$ 
	- En donde  debe ser un operador de comparación: 
		- $=, \ne$
		- >, $\ge$, <, $\le$ (sólo para atributos cuyos dominios están ordenados) 
	- Las operaciones entre predicados admitidas son $\wedge, \vee, \neg$. 
	- Se utilizan los cuantificadores con las mismas reglas que en el CRT (cálculo relacional de tuplas).
	- Ejemplo:
	- Liste los nombres de los países que jugaron el Mundial 2022.
	- $\{n|(\exists s)(\exists g)(\exists c)(NationalTeams(s,n,g,c))\}$
	- Vemos que en este caso ya no tratamos con tuplas, sino únicamente con los valores de los atributos por separado 