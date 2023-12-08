# Ejercicio 1

## Consigna

Para las siguientes planificaciones: 
- Dibujar los grafos de precedencia 
- Listar los conflictos 
- Determinar cuáles son serializables 

**a)**  bT1; bT2; bT3; RT1(X); RT2(Z); RT1(Z); RT3(X); RT3(Y); WT1(X); WT3(Y); RT2(Y); WT2(Z); WT2(Y); cT1; cT2; cT3; 

**b)** bT1; bT2; bT3; RT1(X); RT2(Z); RT3(X); RT1(Z); RT2(Y); RT3(Y); WT1(X); WT2(Z); WT3(Y); WTY2(Y); cT1; cT2; cT3;

## Resolución

### a)

Vemos en una tabla la ejecución de las diferentes transacciones

| $T_1$ | $T_2$ | $T_3$ |
| - - | - - | - - |
|$b_{T_1}$|      |      |
|      |$b_{T_2}$|      |
|      |      |$b_{T_3}$|
|   $R_{T_1}(X)$   |      |      |
|      |   $R_{T_2}(Z)$   |      |
|   $R_{T_1}(Z)$   |      |      |
|      |      |   $R_{T_3}(X)$   |
|      |      |   $R_{T_3}(Y)$   |
|   $W_{T_1}(X)$   |      |      |
|      |      |   $W_{T_3}(Y)$   |
|      |   $R_{T_2}(Y)$   |      |
|      |   $W_{T_2}(Z)$   |      |
|      |   $W_{T_2}(Y)$   |      |
|$c_{T_1}$|      |      |
|      |$c_{T_2}$|      |
|      |      |$c_{T_3}$|


Vemos que los conflictos presentes son: 
- $R_{T_3}(X), W_{T_1}(X)$
- $R_{T_3}(Y), W_{T_2}(Y)$
- $W_{T_3}(Y), R_{T_2}(Y)$
- $W_{T_3}(Y), W_{T_2}(Y)$
- $R_{T_1}(Z), W_{T_2}(Z)$

Con lo cual, el grafo de precedencia quedaría de la siguiente forma:

![[Pasted image 20231030150045.png]]

Como vemos, no hay ciclos, lo que nos indica que **es serializable por conflictos**. El orden de ejecución sería $T_3 \to T_1 \to T_2$.

### b)

Vemos en una tabla la ejecución de las diferentes transacciones

| $T_1$ | $T_2$ | $T_3$ |
| - - | - - | - - |
|$b_{T_1}$|      |      |
|      |$b_{T_2}$|      |
|      |      |$b_{T_3}$|
|  $R_{T_1}(X)$  |    |    |
|    |   $R_{T_2}(Z)$ |    |
|    |    |  $R_{T_3}(X)$  |
|  $R_{T_1}(Z)$  |    |    |
|    |  $R_{T_2}(Y)$  |    |
|    |    |  $R_{T_3}(Y)$  |
|  $W_{T_1}(X)$  |    |    |
|    |  $W_{T_2}(Z)$  |    |
|    |    |  $W_{T_3}(Y)$  |
|    |  $W_{T_2}(Y)$  |    |
|$c_{T_1}$|      |      |
|      |$c_{T_2}$|      |
|      |      |$c_{T_3}$|

Vemos que los conflictos presentes son: 
- $R_{T_3}(X), W_{T_1}(X)$
- $R_{T_1}(Z), W_{T_2}(Z)$
- $R_{T_2}(Y), W_{T_3}(Y)$
- $R_{T_3}(Y), W_{T_2}(Y)$
- $W_{T_3}(Y), W_{T_2}(Y)$

Con lo cual, el grafo de precedencia quedaría de la siguiente forma:

![[Pasted image 20231030152154.png]]

Podemos apreciar un ciclo entre $T_2$ y $T_3$, con lo cual este solapamiento **no** es serializable.

# Ejercicio 2

## Consigna

“Los amigos de mis amigos son mis amigos.” 
Marco Sacherberg quiere evaluar la exactitud del conocido refrán, y para ello utilizará datos de una red social a la que tiene acceso. Dispone en particular de las siguientes tablas: 
- Usuarios(cod usuario, nombre, localidad) 
- Amistades(cod usuario 1, cod usuario 2) 
En esta última tabla, cada relación de amistad a ∼ b se guarda en ambos sentidos, es decir, como par (a, b) y como par (b, a). 
Escriba una consulta en Cálculo Relacional de Tuplas que permita encontrar los códigos de usuario de las personas que cumplen con que “los amigos de sus amigos son también sus amigos” sin excepciones. 
Símbolos: ∃, ∄, ¬, ∧, ∨, ̸=, ≤, ≥

## Resolución

$$ \begin{align} 
&\{U_1.cod\_usuario | \\
&Usuarios(U_1) \wedge (\not \exists U_2) \\
&\qquad (Usuarios(U_2) \wedge (\exists A)\\
&\qquad \qquad (Amistades(A) \wedge A.cod\_usuario\_1 = U_1.cod\_usuario \wedge \\
&\qquad \qquad A.cod\_usuario\_2 = U_2.cod\_usuario) \\
&\qquad \wedge (\exists U_3) \\
&\qquad \qquad (Usuarios(U_3) \wedge (\exists A_1) \\
&\qquad \qquad \qquad (Amistades(A_1) \wedge A_1.cod\_usuario\_1 = U_2.cod\_usuario \wedge \\
&\qquad \qquad \qquad A_1.cod\_usuario\_2 = U_3.cod\_usuario)\\
&\qquad \qquad \wedge (\not \exists A_2) \\
&\qquad \qquad \qquad (Amistades(A_2) \wedge A_2.cod\_usuario\_1 = U_1.cod\_usuario \wedge \\
&\qquad \qquad \qquad A_2.cod\_usuario\_2 = U_3.cod\_usuario)\\
&\qquad \qquad )\\
&\qquad )\\
\}
\end{align} $$

# Ejercicio 3

## Consigna

Sea el siguiente log de un sistema que usa *undo/redo* logging. Cuál es el valor de los items A, B, C, D, E, F y G en disco después de la recuperación si la falla se produce: 
	a) Justo antes de la linea 19 
	b) Justo antes de la linea 24 
	c) Después de la liınea 24

![[Pasted image 20231030174055.png]]

## Resolución

### a) Justo antes de la linea 19 

Justo antes de la línea 19 las transacciones que hicieron commit son $T_1, T_2$ y $T_3$, mientras que la única que no hizo commit fue $T_4$.

Tenemos un Start CKPT pero no un END CKPT, por lo cual nada nos garantiza que los valores antes del Start estén volcados a disco.

Al reiniciarse el equipo:
- $T_4 \to$ Como no hizo commit, se le hace el UNDO. 
	- G = 110
	- F = 10 
- $T_1 \to$ Hizo commit, por lo cual hacemos un REDO de las instrucciones
	- A = 70
	- B = 130
- $T_2 \to$ Hizo commit, por lo cual hacemos un REDO de las instrucciones
	- C = 70
	- D = 40
- $T_3 \to$ Hizo commit, por lo cual hacemos un REDO de las instrucciones
	- E = 60

Los valores de los ítems después de la recuperación son:
- A = 70
- B = 130
- C = 70
- D = 40
- E = 60
- F = 10
- G = 110

### b) Justo antes de la línea 24

Justo antes de la línea 24 las transacciones que hicieron commit son $T_1, T_2$ y $T_3$, mientras que las que no hicieron commit son $T_4$ y $T_5$.

Debido al START CKPT de la línea 12 y END CKPT de la línea 22, sabemos que las modificaciones a los ítems hechas por $T_2$ y $T_3$ ya están en disco antes del Start CKPT ya están en disco, por lo que no las tendríamos que rehacer. 

Al hacer el checkpoint, los valores de los ítems se vuelcan a disco, quedando:

- A = 70
- B = 130
- C = 20
- D = 40
- E = 60

Al reiniciarse el equipo:
- $T_1 \to$ Hizo commit antes del checkpoint, por lo que está guardada en disco.
- $T_4 \to$ Como no hizo commit, se le hace el UNDO. 
	- G = 110
	- F = 10
- $T_5 \to$ Como no hizo commit, se le hace el UNDO. 
	- C = 70
- $T_2 \to$ Hizo commit, por lo cual hacemos un REDO de las instrucciones después del checkpoint, pues las de antes del checkpoint sí fueron volcadas a memoria.
	- C = 70
- $T_3 \to$ Hizo commit, por lo cual hacemos un REDO de las instrucciones después del checkpoint, pues las de antes del checkpoint sí fueron volcadas a memoria.
	- No altera ítems después del checkpoint.

Los valores de los ítems después de la recuperación son:
- A = 70
- B = 130
- C = 70
- D = 40
- E = 60
- F = 10
- G = 110
### c) Después de la línea 24

Después de la línea 24 las transacciones que hicieron commit son $T_1, T_2, T_3$ y $T_4$, mientras que la única que no hizo commit fue $T_5$.

Debido al START CKPT de la línea 12 y END CKPT de la línea 22, sabemos que las modificaciones a los ítems hechas por $T_2$ y $T_3$ ya están en disco antes del Start CKPT ya están en disco, por lo que no las tendríamos que rehacer. 

Al hacer el checkpoint, los valores de los ítems se vuelcan a disco, quedando:

- A = 70
- B = 130
- C = 20
- D = 40
- E = 60

Al reiniciarse el equipo:
- $T_1 \to$ Hizo commit antes del checkpoint, por lo que está guardada en disco.
- $T_5 \to$ Como no hizo commit, se le hace el UNDO. 
	- C = 70
- $T_4 \to$ Hizo commit, por lo cual hacemos un REDO de las instrucciones después del checkpoint. 
	- G = 10
	- F = 150
- $T_2 \to$ Hizo commit, por lo cual hacemos un REDO de las instrucciones después del checkpoint, pues las de antes del checkpoint sí fueron volcadas a memoria.
	- C = 70
- $T_3 \to$ Hizo commit, por lo cual hacemos un REDO de las instrucciones después del checkpoint, pues las de antes del checkpoint sí fueron volcadas a memoria.
	- No altera ítems después del checkpoint.

Los valores de los ítems después de la recuperación son:
- A = 70
- B = 130
- C = 70
- D = 40
- E = 60
- F = 140
- G = 10