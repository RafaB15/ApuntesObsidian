# Ejercicio 1

## **Enunciado:**

Considere la relación *R(A, B, C, D, E)* con el conjunto de dependencias funcionales: *F = {B → C, C → BE, ADE → CB, E → CD}*. Hallar el conjunto minimal $F_{min}$ equivalente al conjunto dado *F* y todas las claves candidatas de *R*. Aplique los algoritmos correspondientes vistos en clase, detallando todos los pasos.

## **Resolución:**

### Conjunto Minimal 

Aplicamos el algoritmo para hallar el conjunto minimal.

1. Pasar a forma canónica

$F = \{B \to C, C \to B, C \to E, ADE \to C, ADE \to B, E \to C, E \to D\}$

2. Ahora eliminamos los atributos innecesarios de la parte izquierda. Para hacer esta parte, primero calculemos las clausura de los atributos.

- $A^+ =\{A\}$
- $B^+ =\{B,C,E,D\}$
- $C^+ =\{C,B,E,D\}$
- $D^+ =\{D\}$
- $E^+ =\{E,C,D,B\}$

Vemos que la única dependencia funcional en donde el implicante tiene múltiples atributos es *ADE*. A se implica a sí mismo, por lo que es necesario, pero vemos que *E* implica  a *D*, con lo que podemos evitar escribirlo, quedando las dependencias funcionales de la siguiente manera.

$F = \{B \to C, C \to B, C \to E, AE \to C, AE \to B, E \to C, E \to D\}$

3. Eliminamos las dependencias funcionales redundantes.

Para este paso, quitamos las diferentes dependencias funcionales y vemos si la clausura de los implicantes se redujo. 

Ver que:

- $AE^+ =\{A,E,C,D,B\}$

Quitamos:
- $B \to C$
	- $B'^+ =\{B\}$ Se redujo
- $C \to B$
	- $C'^{+}=\{C,E,D\}$ Se redujo
- $C \to E$
	- $C''^{+}=\{C,B\}$ Se redujo
- $AE \to C$
	- $AE'^+ =\{A,E,C,D,B\}$ Se quedó igual, podemos quitar esta *df*
- $AE \to B$
	- $AE''^+ =\{A,E,C,D,B\}$ Se quedó igual, podemos quitar esta *df*
- $E \to C$
	- $E'^+ =\{E, D\}$ Se redujo
- $E \to D$
	- $E''^+ =\{E,C,B\}$ Se redujo

Entonces, después de aplicar el algoritmo, llegamos a que

$$F_{min} = \{B \to C, C \to B, C \to E,E \to C, E \to D\}$$
### Claves Candidatas

Ahora seguimos los pasos para encontrar las claves candidatas de esta relación. Ya tenemos el conjunto minimal de dependencias, entonces seguimos los siguientes pasos
- El conjunto de atributos de cálculo inicial será $C_a = \{A,B,C,D,E\}$ 

- Buscamos atributos independientes.

	Vemos que el atributo *A* no está presente en las *df*, por lo que

$$Indep = \{A\}$$
	Lo sacamos de $C_a$, quedando $C_a = \{B,C,D,E\}$ 

- Buscamos los atributos equivalentes

	Podemos notar que, dadas las *df* $B \to C$, $C\to B$, $E \to C$ y $C \to E$, *B, C,* y *E* son equivalentes, cosa que podemos corroborar dado que sus clausuras son iguales. Nos quedaremos solo con uno de estos para los siguientes cálculos, el cual será *E*. 

	$C_a = \{E,D\}$ 

	Calculamos la proyección de $F_{min}$ en $C_a$
	$F_C =\{E \to D\}$

- Ahora construimos una clave tentativa $K_{tent}$ que tiene solo a los valores a la izquierda de $F_C$, siendo $K_{tent} = E$. 
- Como $K_{tent}^+ = E^+= \{E, D\} = C_a$, entonces esta es la clave.
- Agregando el atributo independiente y los atributos equivalentes, tenemos las siguientes claves candidatas:
	- $CK_1 = \{A, E\}$
	- $CK_2 = \{A, B\}$
	- $CK_3 = \{A, C\}$

# Ejercicio 2

## Enunciado:

Dada la relación *R(A, B, C, D, E, G, H)* con el conjunto minimal de dependencias funcionales: *F = {AD → C, G → H, BG → E, CH → B}*. 
Con clave candidata *{ADG}*. Suponga que aplicamos el algoritmo de descomposición en FNBC y elegimos para el primer paso la *df CH → B*. Como serían los esquemas resultante de este paso? En que forma normal se encuentran? Como debería continuar el algoritmo? (para responder esto último sólo explique como sería).

## Resolución

Al seguir el algoritmo de descomposición en FNBC y elegir $CH \to B$ como la dependencia que queremos separar, vamos a dividir nuestra relación universal en dos nuevos esquemas.

**Rama izquierda:**

Al haber elegido la dependencia funcional $CH \to B$, la nueva tabla va a tener que tener los valores *C* y *H* como clave primaria, así como todos los elementos implicados por estos atributos

$CH^+ = \{C, H, B\}$

Nuestra nueva relación es entonces

$R_1(C, H, B)$
$F_1 = \{CH \to B\}$ 

**Rama derecha**:

En la rama derecha pondremos todos los atributos que no están implicados en las dependencias funcionales de la rama izquierda, así como la clave primaria de la rama izquierda.

$R_2(A,C,D,E,G,H)$ 
$F_2 = \{AD \to C, G \to H\}$ 

Podemos notar que, como puede suceder al aplicar el algoritmo de descomposición a *FNBC*, la dependencia $BG \to E$ no terminó en ninguna de las ramas, por lo que a pesar de que mantenemos la información, se perdería esa dependencia funcional.

En cuanto a la forma normal en la que se encuentran las ramas, podemos notar que la **rama izquierda** se encuentra efectivamente en **FNBC**, dado que no existen dependencias transitivas.

En cuanto a la rama de la derecha, vemos que esta se encuentra en **1FN**, debido a que, al ser la única clave candidata *ADG*, y tener *C* y *H* dependencias parciales de la clave, no se cumple **2FN**. 

Lo siguiente que tendríamos que hacer para la rama derecha, dado que la izquierda **si** terminó siendo **FNBC**, es elegir alguna de las dependencias funcionales de $R_2$ ($F_2$) y repetir el proceso que acabamos de hacer hasta que todas las hojas estén en la forma normal Boyce-Cood.

# Ejercicio 3

## Enunciado

Una biblioteca guarda, para cada uno de sus préstamos, los siguientes datos: Numero, nombre, apellido, dirección y teléfono del socio - ISBN del libro - Título del libro - Código del autor del libro - Nombre y apellido del autor del libro - Fecha de nacimiento y de muerte del autor del libro - Tipo de autor(\*) - Número de páginas del libro - Cantidad de días por los que se presta el libro - Fecha en la que se presta el libro - Fecha esperada de devolución - Fecha real de devolución

Condiciones: 
a) Cada socio tiene un número único que lo identifica. 
b) Se registra un solo domicilio y un solo teléfono por cada socio. 
c) Cada libro tiene un ISBN único que lo identifica. Suponer que la biblioteca solo tiene un ejemplar de cada libro. 
d) Cada autor se identifica con un número único. 
e) Un libro tiene siempre al menos un autor. Puede tener más de uno. No hay libros de autores desconocidos. 
f ) Un socio puede sacar muchos libros, pero solo de a uno por vez (no se le presta un nuevo libro hasta que no haya devuelto el anterior). 
g) Para cada libro, se decide por cuántos días se prestará. Esta cantidad de días no depende del socio, sino del libro. 
h) Un mismo lector puede llevarse varias veces el mismo libro. 

Si surgen dudas respecto a otras condiciones, registrelas por escrito, adopte una interpretación y aplíquela en el ejercicio. 
(\*) Un autor puede ser: autor principal, coautor, prologuista, traductor o compilador. Un mismo autor puede ser, por ejemplo, prologuista de un libro y compilador de otro. 

a) Escriba el esquema universal (única relación que contenga todos los atributos) que se ajuste al enunciado. 
b) Dar un conjunto de dependencias funcionales. 
c) Determinar claves del esquema. No hace falta que utilice el algoritmo. 
d) En que forma normal se encuentra? si esta en una forma inferior, llevarlo a 3FN.

## Resolución

### Esquema universal

El esquema universal en donde están todos los atributos del eneunciado sería el siguiente:

*R(num_socio, nombre_socio, apellido_socio, dirección, teléfono, ISBN, título, cod_autor, nombre_autor, apellido_autor, nacimiento_autor, muerte_autor, tipo_autor, num_paginas, plazo_prestamo, fecha_prestamo, fecha_devolución_esperada, fecha_devolución_real)*

### Dependencias funcionales

- $num\_socio \to nombre\_socio, apellido\_socio, dirección, teléfono$
- $ISBN \to título, num\_paginas, plazo\_prestamo$
- $cod\_autor \to nombre\_autor, apellido\_autor, nacimiento\_autor, muerte\_autor$
- $plazo\_prestamo, fecha\_prestamo \to fecha\_devolución\_esperada$
### Claves del esquema

Podemos ver que los atributos independientes de la relación son *fecha_devolución_real y tipo_autor*. Además, vemos que los atributos que no son implicados por las dependencias son *num_socio, ISBN, cod_autor, fecha_prestamo*, y dado que la clausura de estos es igual a todos los atributos de la relación, entonces nuestra única clave será:
$PK = \{num\_socio, ISBN, cod\_autor, fecha\_prestamo, fecha\_devolución\_real, tipo\_autor\}$ 
### Forma normal

Este esquema se encuentra en **1FN**, debido a que hay muchos atributos no primos que dependen parcialmente de la clave primaria, cosa que no permite **2FN**.

Vamos a utilizar el algoritmo para normalizar a **3FN**. 

1. Necesitamos un cubrimiento minimal de las dependencias
	Dado que nuestras dependencias no tienen atributos innecesarios a derecha y sacarlas supondría no poder recuperar esas dependencias funcionales (no hay df redundantes), entonces nuestro cubrimiento minimal de las df sería

$$\begin{align} 
F_{min} = \{\{num\_socio \to nombre\_socio, apellido\_socio, dirección, teléfono\},\\
\{ISBN \to título, num\_paginas, plazo\_prestamo\}, \\
\{cod\_autor \to nombre\_autor, apellido\_autor, \\ nacimiento\_autor, muerte\_autor\},\\
\{plazo\_prestamo, fecha\_prestamo \to fecha\_devolución\_esperada\}
\end{align}$$

2. Creamos un esquema por cada implicante en las dependencias funcionales

-  $num\_socio \to nombre\_socio, apellido\_socio, dirección, teléfono$
	- $R_1(num\_socio, nombre\_socio, apellido\_socio, dirección, teléfono)$
	- $F_1 = \{num\_socio \to nombre\_socio, apellido\_socio, dirección, teléfono\}$
- $ISBN \to título, num\_paginas, plazo\_prestamo$
	- $R_2(ISBN, título, num\_paginas, plazo\_prestamo)$
	- $F_2 = \{ISBN \to título, num\_paginas, plazo\_prestamo\}$
- $cod\_autor \to nombre\_autor, apellido\_autor, nacimiento\_autor, muerte\_autor$
	- $R_3(cod\_autor, nombre\_autor, apellido\_autor, nacimiento\_autor, muerte\_autor)$
	- $F_3 = \{cod\_autor \to nombre\_autor, apellido\_autor, nacimiento\_autor, muerte\_autor\}$
- $plazo\_prestamo, fecha\_prestamo \to fecha\_devolución\_esperada$
	- $R_4(plazo\_prestamo, fecha\_prestamo, fecha\_devolución\_esperada)$ 
	- $F_4 = \{plazo\_prestamo, fecha\_prestamo \to fecha\_devolución\_esperada\}$

3. Dado que en ninguna de las tablas se encuentra la única clave candidata de *R*, creamos una nueva tabla que la contenga.

- $R_5(num\_socio, ISBN, cod\_autor,fecha\_prestamo, fecha\_devolución\_real, tipo\_autor)$

4. Como los atributos de ninguna relación están incluidos en la de otra, entonces estas 5 relaciones son el resultado final.

Es entonces como normalizamos la relación universal *R* a **3FN**, teniendo como resultado las relaciones $R_1, R_2, R_3, R_4$ y $R_5$, con sus respectivas dependencias funcionales.