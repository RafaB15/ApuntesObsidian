Si tengo el sistema $Ax = b$ con $b\not\in \text{Col}(A)$ podemos buscar un vector $\hat{x}$  tal que $A\hat{x} = P_{\text{Col}(A)}(b)$, es decir que $\text{dist}(A\hat{x},b)$ sea la "menor distancia".

Lo soluciono usando las **ecuaciones normales**:

$$
\text{A}^TA\hat{x} = \text{\=A}^Tb
$$

Básicamente, proyectamos B en las columnas de A para que si haya un resultado, y ese resultado será la solución más cercana.

Dada $A \in \Bbb K^{m \text{ x } m}$ y $b \in \Bbb K^m$, se dice que $\hat x$ es la **solución por mínimos cuadrados** de $Ax =b$ si $A \hat x$ **realiza** la mínima distancia a $b$, o sea

                                      $dist(A \hat x,b) \le dist(Ax, b) \iff A \hat x = P_{Col(A)} (b)$

Se llama error cuadrático media a la diferencia:

                                                                   $\text{ECM} = \| b - A \hat x \| ^2$ 

- Observaciones
    - El problema de cuadrados mínimos siempre tiene solución.
    - $\text{Nul}(\text{\=A}^TA) = \text{Nul}(A)$
    - $\text{rg}(\text{\=A}^TA) = \text{rg}(A)$, si $\text{rg}(A) = n$ se dice que $A$ tiene rango columna máximo.
    - Si $A$ es de tango columna máximo, $\text{\=A}^TA\hat{x} = \text{\=A}^Tb\iff \hat{x} = (\text{\=A}^TA)^{-1}\text{\=A}^Tb$

**Definición**: Si $A \in \mathbb{K^{m\times n}}$, $\text{rg}(A) = n$, se llama pseudoinversa de $A$  a la matriz

 $A^{\#} = (\text{\=A}^TA)^{-1}\text{\=A}^T$  .

- Propiedades
    - $A^{\#}A = (\text{\=A}^TA)^{-1} \text{\=A}^TA = (\text{\=A}^TA)^{-1} (\text{\=A}^TA) = I_n$
    - $AA^{\#}$ es la matriz de la proyección ortogonal sobre $\text{Col}(A)$
    

## Conclusión:

Sean $(\Bbb R^n, \langle .,.\rangle)$ y $(\Bbb R^m, \langle .,.\rangle)$ los espacios euclídeos canónicos de dimensión $n$ y $m$ respectivamente. Sea $A \in \Bbb R^{m \text{ x }n}$ y $b \in \Bbb R^m$. Entonces son equivalentes:

- $\hat x \in \Bbb R^n$ es una solución de mínimos cuadrados de la ecuación $Ax = b$.
- $\| A \hat x -b\| = \text{min}\{\|Ax-b\|:x\in \Bbb R^n \}$ ó equivalentemente $\| A \hat x -b\| \le \| A x -b\|$ para todo $x \in \Bbb R^n$.
- $\hat x \in \Bbb R^n$ es una solución de la ecuación $A x = P_{Col(A)} (b)$, es decir $A \hat x = P_{Col(A)} (b)$.
- $\hat x \in \Bbb R^n$ es una solución de **ecuación normal $\overline{A}^TAx = \overline{A}^Tb$,** es decir $\overline{A}^TA\hat x = \overline{A}^Tb$.

En este caso, si $\hat x_p$ es una solución de mínimos cuadrados de $Ax = b$ entonces todas las soluciones de mínimos cuadrados de $Ax=b$ son 

                                                                   $\hat x = \hat x_p + z$

con $z \in \text{nul}(A)$. En particular, eciste una única solución de mínimos cuadrados de $Ax = b$ si y sólo si $\text{nul}(A) = \{0\}$.

### Problema que mejor ajusta

Si tengo un conjunto de datos y supongo una relación entre las variables puedo buscar una curva que ajuste estos datos.

Si elijo una curva lineal $y = mx + b$

$$
\begin{cases} mx_1 + b = y_1 \\ mx_2 + b = y_2 \\ ... \\ mx_n+b = y_n\end{cases} \to \begin{bmatrix}x_1 & 1 \\ x_2 & 1 \\ ... & ... \\ x_n & 1\end{bmatrix}\begin{bmatrix}m\\b\end{bmatrix} = \begin{bmatrix}y_1 \\ y_2 \\ ... \\y_n\end{bmatrix}
$$

y puedo plantearlo usando los mínimos cuadrados.

$$
A^TA \begin{bmatrix}m\\b\end{bmatrix}= \begin{bmatrix}x_1 & x_2 & ... &x_n \\1 & 1 & ... & 1\end{bmatrix} \begin{bmatrix}x_1 & 1 \\ x_2 & 1 \\ ... & ... \\ x_n & 1\end{bmatrix}\begin{bmatrix}m\\b\end{bmatrix} 
$$