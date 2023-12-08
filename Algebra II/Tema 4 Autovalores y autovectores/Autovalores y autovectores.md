## Calcular potencias de una matriz:

Es fácil calcular la potencia n-ésima de una matriz diagonal, pues es solo elevar a la n cada elemento de esta.

                        $\displaystyle D = diag(\lambda_1, \lambda_2, \dots ,\lambda_n)=\begin{bmatrix}\lambda_1 & 0 & 0 & \dots & 0 \\ 0 & \lambda_2 & 0 & \dots & 0\\0 & 0 & \lambda_3 & \dots & 0 \\ \vdots & \vdots & \vdots & \ddots & \vdots\\ 0 & 0 & 0 &\dots & \lambda_n\end{bmatrix}$ 

                                              

                                                    $\displaystyle D^k = diag(\lambda_1^k, \lambda_2^k, \dots ,\lambda_n^k)$

Para calcular la potencia n-ésima de una matriz cuadrada de la forma $A \in \Bbb K^{\text{n x n}}$, la podemos factorizar de siguiente manera

                                                                   $A = Q\ D\ Q^{-1}$ 

con $Q$ una matriz inversible $\in \Bbb K^{\text{n x n}}$ y  $D = diag(\lambda_1, \lambda_2, \dots ,\lambda_n) \in \Bbb K^{\text{n x n}}$. 

En general tenemos que si $n \in \Bbb N$:

                                                   $A = Q\ D\ Q^{-1}  \implies A^n = Q\ D^n\ Q^{-1}$ 

La relación que tienen  que cumplir estas matrices para que se cumpla esta ecuación es

                                $A = Q\ D\ Q^{-1}  \iff AV_i = \lambda V_i,$  donde $V_i = \text{Col}_i(Q)$

## **Definición:**

Sea $A \in \Bbb K^{\text{n x n}}$, un **autovalor** de $A$ es un escalar $\lambda \in \Bbb K$ tal que existe $v\in \Bbb K ^\text{n}$, $v\not= 0$ que cumple $Av=\lambda v$. Se dice que $v$ es **autovector.** 

## Encontrar autovalores y autovectores:

                                          $Av = \lambda v \iff (\lambda v - Av)=0_{\Bbb K ^\text{n}}$ y $v \not= 0_{\Bbb K ^\text{n}}$.

                                                                        $(\lambda \text{I} - A)v = 0_{\Bbb K ^\text{n}}$ y $v \not= 0_{\Bbb K ^\text{n}}$

Esto quiere decir que este sistema lineal homogéneo tiene infinitas soluciones, pues sabemos que hay una solución que es no trivial.

Como hay infinitas soluciones, entonces no es inversible, por lo que el determinante de la matriz tiene que ser cero.

Entonces para calcular autovalores y autovectores para $A \in \Bbb K^{\text{n x n}}$

- Buscamos $\lambda \in \Bbb K$ tal que $\text{det}(\lambda\text{I} - A) = 0$.
- Para cada $\lambda$, los autovectores de $A$ asociados a $\lambda$ son $v \not= 0_{\Bbb K^n}/(\lambda\text{I} - A)v = 0_{\Bbb K^n} \iff v \in \text{Nul}(\lambda\text{I} - A)$

El conjunto de todos los autovalores de A se conoce como espectro de A y se designa mediante

                                                                        $\sigma(A)$

El conjunto de autovectores de $A$ asociados a cada autovalor $\lambda_0$ son los vectores no nulos, solución del sistema homogéneo $(\lambda\text{I} - A)X = 0_{\Bbb K^n}$. Se llama **autoespacio de A asociado a $\lambda_0$ al subespacio $\text{Nul}(\lambda_0\text{I} - A)$ y se nota:**

              

                                                   $S_{\lambda = \lambda_0}= \{v \in \Bbb K^n/Av=\lambda_0v\}$

                      

- **Definiciones**
    - Se dice que A es **diagonalizable** si existe **$Q \in \Bbb K^{\text{n x n}}$** inversible y $D = diag(\lambda_1, \lambda_2, \dots ,\lambda_n)\in \Bbb K^{\text{n x n}}$ tal que $A= Q \ D\ Q^{-1}$.
    - Se llama **polinomio característico de $A$** , al polinomio de grado $n$, $P_A(\lambda) = \text{det} (\lambda\text{I} - A)$.
    - Si $\lambda_0$  es autovalor de $A$, se llama **multiplicidad algebraica** de $**\lambda_0$,** a la multiplicidad de $\lambda_0$ como raíz del polinomio característico. (Se nota: $m_{\lambda}$)
    - Si $\lambda_0$  es autovalor de $A$, se llama **multiplicidad geométrica** de $**\lambda_0$,** a la dimensión de su autoespacio asociado. Notamos: $\mu_{\lambda} = \text{dim(Nul(}\lambda_0\text{I} -A))$.
- **Observaciones**
    - Si $\lambda_0 \in  \Bbb K$ es autovalor de $A \implies \mu_{\lambda} \ge 1$
    - Si $\lambda = 0$ es autovalor de $A \implies S_{\lambda = 0}=\text{Nul}(A)$.
    - Si $A$ es inversible $\lambda \not= 0, \ \forall\ \lambda$  autovalor de $A$.
    - A es diagonalizable si existe una base de $\Bbb K^{\text{n}}$ formada por autovectores de A.
    - Los autovalores de $A$ son las raíces de su polinomio característico.
    - Sea $\{v_1,v_2,\dots,v_k\}$ un conjunto de autovectores de $A$ asociados respectivamente a los autovalores $\lambda_1, \lambda_2,\dots,\lambda_k$, tal que $(\lambda_i \not= \lambda_j \ \forall \ i \not= j ) \implies \{v_1,v_2,\dots,v_k\}$ es l.i.
    - $\mu_{\lambda}$ (multiplicidad geométrica) $\le m_{\lambda}$  (multiplicidad algebraica).

## Resultados importante:

Si una matriz $A \in \Bbb K^{\text{n x n}}$ tiene $n$ autovalores distintos en $\Bbb K \implies A$ es **diagonalizable**.

Si algún autovalor tiene multiplicidad algebraica mayor que uno tendremos que ver si podemos encontrar asociados a él tantos autovectores l.i. como su multiplicidad algebraica para que sea diagonalizable. O sea, se debe cumplir que **multiplicidad algebraica = multiplicidad geométrica** para cada autovalor de $A$.

## Propiedades sobre autovalores:

Teniendo $A \in \Bbb K^{\text{n x n}}$

- $\displaystyle \text{det}(A) = \prod_{i = 1}^{n} \lambda_i$. (Se consideran los autovalores con repetición.)
- $\displaystyle \text{tr}(A) = \sum_{i = 1}^{i=n} \lambda_i$. (Se consideran los autovalores con repetición.)
- Si $\lambda$  autovalor de $A$ asociado al autovector $v$:
    - $(\lambda^{k} + t)$ es autovalor de $(A^k + t\text{I})$ asociado al autovector $v$.
    - Si $A$ es inversible $\implies \frac{1}{\lambda}$ de $A^{-1}$ asociado al autovector $v$.
- Si $\lambda$   autovalor de $A \implies \lambda$ es autovalor de $A^{T}$. (Los autovectores no tienen porqué ser los mismos.)