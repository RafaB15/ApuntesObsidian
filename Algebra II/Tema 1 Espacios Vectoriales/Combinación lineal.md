Un vector $w \in V-K$ espacio vectorial, es **combinación lineal** de un conjunto de vectores $v_1, v_2,...,v_n$ en $V$, si existen escalares, $\lambda_1, \lambda_2, ...,\lambda_n \in K$ tales que:

                                          $\displaystyle w = \lambda_1 v_1+\lambda_2 v_2+...+\lambda_n v_n= \underbrace{\sum_{i=1}^{n} \lambda_i v_i}_{\text{notación}}$

$gen\{ v_1,v_2,...,v_n\}$ representa el conjunto de todas las combinaciones lineales posibles entre los vectores $v_1,v_2,...,v_n$.

# Dependencia e independencia lineal

Se dice que un conjunto de dos o más vectores $\{v_1,v_2,...,v_n\} \subset V-K$ espacio vectorial, es linealmente dependiente (ld) si alguno de sus elementos es combinación lineal de los demás. Si el conjunto está formado por único vector $v_1$, se dice que el linealmente dependiente solo si $v_1=O_{_V}$. Cuando esto no sucede, se dice que el conjunto es linealmente independiente.

Será linealmente independiente si la única manera de escribir al elemento nulo es que todos los escalares sean 0.

Equivalentemente se puede decir, que un conjunto $\{v_1,v_2,...,v_n\} \subset V-K$ espacio vectorial es linealmente independiente si:

                         $\lambda_1 v_1 +\lambda_2 v_2 +... +\lambda_n v_n = O_{_V} \implies \lambda_1 = \lambda_2 = ... = \lambda_n =0$ 

## Observaciones:

- Todo conjunto que contenga a $O_{_V}$  es ld.
- Si un conjunto tiene dos elementos $\{u_1,u_2\}$ es ld $\exists \  k \in K / u_2 = ku_1$.
- Si $\{u_1,u_2,...,u_n\}$ es un conjunto de vectores y $u_k$ es combinación lineal de los demás vectores del conjunto, entonces:

                                          $gen\{u_1,u_2,...,u_k\} = gen\{u_1,u_2,...,u_{k-1}\}$