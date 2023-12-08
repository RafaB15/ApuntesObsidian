Si $B = \{v_1,v_2,...,v_n\} \subset V$ es una base de $V$ siempre se cumple:

Para cada $v \in V$ existen únicos escalares $\alpha_1,\alpha_2,...,\alpha_n \in K$ tal que:$v = \alpha_1v_1 + \alpha_2v_2 + ...+ \alpha_nv_n$ (la descomposición de un vector con respecto a una base es única).

Para cada elemento de $v \in V$, existe una única n-upla en $K^n$ formada por los escalares $\alpha_1,\alpha_2,...,\alpha_n$  que participan en su descomposición con respecto a la base.

Definimos la función: $[\ .\ ]^B : V \to K^n$ (**coordenadas con respecto a la base $B$** ).

Con la fórmula $[v]^B =\begin{bmatrix} \alpha_1 \\ \alpha_2 \\ .\\.\\.\\ \alpha_n\end{bmatrix} \iff v = \alpha_1v_1 + \alpha_2v_2 + ...+ \alpha_nv_n$     

                                  

con $\alpha_1, \alpha_2, ... \alpha_n \in K.$

Es una función biyectiva que cumple:

- $[v]^B =\begin{bmatrix} 0 \\ 0 \\ .\\.\\.\\ 0\end{bmatrix} \iff v = O_{_V}$

- $[v+w]^B = [v]^B + [w]^B$
- $[\lambda v]^B = \lambda [v]^B$
- $\{w_1,w_2,...,w_k\}$ es l.i. en $V \iff \{[w_1]^B,[w_2]^B,...,[w_n]^B\}$ es l.i. en $K^n$.

## Matriz de cambio de base:

En un espacio vectorial $V$ consideremos las bases:

$B = \{ v_1,v_2,...,v_n\}$  y $B' = \{ w_1,w_2,...,w_n\}$ 

                                       $[v]^B =\begin{bmatrix} \alpha_1 \\ \alpha_2 \\ .\\.\\.\\ \alpha_n\end{bmatrix}$y también $[v]^{B'} =\begin{bmatrix} \beta_1 \\ \beta_2 \\ .\\.\\.\\ \beta_n\end{bmatrix}$

$[v]^{B'} = [\alpha_1v_1 + \alpha_2v_2 + ...+\alpha_nv_n]^{B'} =\underbrace{ \alpha_1[v_1]^{B'} + \alpha_2[v_2]^{B'}+...+\alpha_n[v_n]^{B'} }_{\text{comb. lineal en }K^n}$

Podemos escribir:

                                 $\displaystyle [v]^{B'} =\underbrace{ \begin{bmatrix} [v_1]^{B'} & [v_2]^{B'} &...&[v_n]^{B'}\end{bmatrix}}_{\text{matriz de nxn}}\begin{bmatrix} \alpha_1 \\ \alpha_2 \\ .\\.\\.\\ \alpha_n\end{bmatrix} = M_B^{B'}[v]^{B}$

                                                       $M_B^{B'}[v]^{B} = [v]^{B'}$

$M_B^{B'} \in K^{n\ x\ m}$ es una matriz inversible y $M_B^{B'} = (M_{B'}^B)^{-1}$