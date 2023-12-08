Si una matriz $A \in \Bbb C^{\text{n x n}}$ no es diagonalizable. entonces no podemos encontrar una matriz diagonal $D$ semejante a $A$, sin embargo, podemos encontrar una matriz más sencilla, diagonal por bloques, semejante a esta matriz $A$.

A estas matrices las llamamos matrices de **Jordan**, que construiremos para matrices de  **$\text{2 x 2}$ y $\text{3 x 3}$.**

Si $A$ es una matriz de $\Bbb C^{\text{n x n}}$ no diagonalizable se cumple alguno de los casos.

## Caso 1:

$A$ tiene un autovalor $\lambda_1$ de multiplicidad algebraica 2 y multiplicidad geométrica 1 y un autovalor $\lambda_2$ de multiplicidad algebraica 1 y multiplicidad geométrica 1.

En este caso podemos probar que $A \sim J_1 = \begin{bmatrix}\lambda_1 & 1 & 0 \\ 0&\lambda_1 & 0 \\ 0 & 0 & \lambda_2\end{bmatrix}$ 

La matriz $J_1$ tiene como autovalores a $\lambda_1$ y $\lambda_2$ y que $\lambda_1$ es un valor de m.a. 2 con $\text{dim}(S_{\lambda_1}) = 1$ y $\lambda_2$ un autvalor simple de $J_1$.

Se prueba entonces que existe $Q$ tal que $A = Q\ J_1 \ Q^{-1}$.

Para encontrar $Q$ hacemos $A = Q\ J_1 \ Q^{-1} \iff AQ = QJ_1$.

Si $Q$ tiene columnas $[V_1|V_2|V_3]$ entonces

                                                   $A\ [V_1|V_2|V_3] = [V_1|V_2|V_3]\ \begin{bmatrix}\lambda_1 & 1 & 0 \\ 0&\lambda_1 & 0 \\ 0 & 0 & \lambda_2\end{bmatrix}$ 

Igualando columna a columna:

$AV_1 = \lambda_1V_1 \implies V_1$ es autovector de $A$ asociado a $\lambda_1$.

$AV_2 = [V_1|V_2|V_3] \ \begin{bmatrix}1 \\ \lambda_1\\ 0\end{bmatrix} = V_1 + \lambda_1V_2 \implies (A - \lambda_1  I)V_2 = V_1$

$AV_3 = \lambda_2V_3\implies V_3$ es autovector de $A$ asociado a $\lambda_2$.

Entonces $V_2$ también lo podemos sacar

                                             $(A - \lambda_1  I)^2V_2 = (A - \lambda_1  I)V_1 = 0_{\Bbb C ^3}$

## Caso 2

$A$ tiene un autovalor $\lambda$ de multiplicidad algebraica 3 y multiplicidad geométrica 1.

En este caso podemos probar que $A \sim J_1 = \begin{bmatrix}\lambda & 1 & 0 \\ 0&\lambda & 1 \\ 0 & 0 & \lambda\end{bmatrix}$ 

Buscamos $Q$ tal que $AQ = QJ_2$

                                    $A\ [V_1|V_2|V_3] = [V_1|V_2|V_3]\ \begin{bmatrix}\lambda & 1 & 0 \\ 0&\lambda & 1 \\ 0 & 0 & \lambda\end{bmatrix}$ 

$AV_1 = \lambda V_1 \implies V_1$ es autovector de $A$ asociado a $\lambda$.

$AV_2 =  V_1 + \lambda V_2 \implies (A - \lambda  I)V_2 = V_1$ 

$AV_3 =  V_2 + \lambda V_3 \implies (A - \lambda  I)V_3 = V_2$ 

para sacar $V_3$

                           $(A - \lambda  I)^3V_3 = (A - \lambda  I)^2V_2 = (A - \lambda  I)V_1 = 0_{}$

A $V_3$  se lo denomina vector propio generalizado.