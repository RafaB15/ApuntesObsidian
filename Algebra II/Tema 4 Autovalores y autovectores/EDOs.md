Resolveremos ecuaciones de la forma 

                                                                   $Y'=AY$ con $A\in \Bbb R^{\text{n x n}}$ 

          

                        $Y(t) = \begin{bmatrix} y_1(t) \\ y_2(t) \\ \vdots \\ y_n(t) \end{bmatrix} , Y'(t) = \begin{bmatrix} y_1'(t) \\ y_2'(t) \\ \vdots \\ y_n'(t) \end{bmatrix}, A = \begin{bmatrix} a_{11} & a_{12} & \dots & a_{1n} \\ a_{21} & a_{22} & \dots & \vdots \\ \vdots & \vdots & \ddots & \vdots \\ a_{n1} & a_{n2} & \dots & a_{nn} \end{bmatrix}$

### Resultados:

- Si $v$ es autovector de $A$ de autovalor $\lambda$, entonces $Y(t) = ve^{\lambda t}$ es solución de $Y'=AY$.
- Sean $v_i$ autovectores de $A$ de autovalor $\lambda_i$. Si $\lambda_k \not= \lambda_r$ entonces $v_ke^{\lambda_k t}$ y $v_re^{\lambda_r t}$, son soluciones linealmente independiente de $Y'=AY$.
- El espacio de soluciones de $Y'=AY$, $A \in \Bbb R^{\text{n x n}}$ es un subespacio de $C^1 (I, \Bbb C^n)$ de dimensión $n$.
- Sea $A$ una matriz de $\text{n x n}$ diagonalizable y sea $\{v_1,v_2,\dots,v_n\}$ una base $\Bbb C^n$ formada por autovectores de $A$ asociados a los autovalores $\lambda_1,\lambda_2,\dots,\lambda_n$. Entonces $\{v_1e^{\lambda_1 t}, v_2e^{\lambda_2 t},\dots, v_ne^{\lambda_n t}\}$ es una base de soluciones de $Y'=AY$.

## Caso A diagonalizable:

Pudiéndose escribir $A$ de la forma $A = PDP^{-1}$ con $D$ una matriz diagonal, con

                     $P=\begin{bmatrix} v_1 & v_2 & v_3 & \dots & v_n \end{bmatrix},\ \  D =\begin{bmatrix}\lambda_1 & 0 & 0 & \dots & 0 \\ 0 & \lambda_2 & 0 & \dots & 0\\0 & 0 & \lambda_3 & \dots & 0 \\ \vdots & \vdots & \vdots & \ddots & \vdots\\ 0 & 0 & 0 &\dots & \lambda_n\end{bmatrix}$

las soluciones serán de la forma

                                                     $\{v_1e^{\lambda_1 t}, v_2e^{\lambda_2 t},\dots, v_ne^{\lambda_n t}\}$

Si los autovalores son complejos tendremos dos soluciones

                                 $Y_1(t) =e^{\lambda t}v = e^{(a+bi)t}v = e^{at}(cos(bt)+sen(bt))v$

                                 $Y_2(t) = e^{\overline \lambda t}\overline v = e^{(a-bi)t}\overline v = e^{at}(cos(bt)-sen(bt))\overline v$ 

Si quisiera tener soluciones reales puedo hacer

                                                    $Y_1(t) + Y_2(t) = 2\text{Re}(Y_1(t))$

                                                   $\displaystyle \frac{Y_1(t) - Y_2(t)}{2i} = \text{Im}(Y_1(t))$

## Caso A no diagonalizable

### $A \in\Bbb R^{\text{2 x 2}}$

En este caso tendremos que usar la matriz de Jordan, pues hay un autovalor de multiplicidad 2 con un autovector.

                                                                   $A = P\ J\ P^{-1}$

                

                                        $J = \begin{bmatrix} \lambda & 1 \\ 0 & \lambda\end{bmatrix}$                         $P = \begin{bmatrix} v_1 & v_2 \end{bmatrix}$

Las soluciones serán generados por

                                                           $\{ e^{\lambda t}v_1,e^{\lambda t} (v_2 + tv_1)\}$

### $A \in \Bbb R^{\text{3 x 3}}$

Tendremos tres situaciones distintas:

### Situación 1:

Un solo autovalor triple y autoespacio asociado de dimensión 1

                                        $J = \begin{bmatrix} \lambda & 1 & 0\\ 0 & \lambda & 1\\ 0&0&\lambda\end{bmatrix}$                         $P = \begin{bmatrix} v_1 & v_2 & v_3\end{bmatrix}$

Las soluciones serán generadas por

                                             $\displaystyle \{ e^{\lambda t}v_1,e^{\lambda t} (v_2 + tv_1),e^{\lambda t}(\frac{t^2}{2}v_1 + tv_2 + v_3) \}$

### Situación 2:

Un solo autovalor triple y autoespacio asociado de dimensión 2

                                        $J = \begin{bmatrix} \lambda & 1 & 0\\ 0 & \lambda & 0\\ 0&0&\lambda\end{bmatrix}$                         $P = \begin{bmatrix} v_1 & v_2 & v_3\end{bmatrix}$

Las soluciones serán generadas por

                                                  $\displaystyle \{ e^{\lambda t}v_1,e^{\lambda t} (v_2 + tv_1),e^{\lambda t}v_3 \}$

### Situación 2:

Un autovalor doble $\lambda_1$  con autoespacio asociado de dimensión 2 y un autovalor simple $\lambda_2$ con autoespacio asociado de dimensión 1.

                                        $J = \begin{bmatrix} \lambda_1 & 1 & 0\\ 0 & \lambda_1 & 0\\ 0&0&\lambda_2\end{bmatrix}$                         $P = \begin{bmatrix} v_1 & v_2 & v_3\end{bmatrix}$

Las soluciones serán generadas por

                                                      $\displaystyle \{ e^{\lambda_1 t}v_1,e^{\lambda_1 t} (v_2 + tv_1),e^{\lambda_2 t}v_3 \}$