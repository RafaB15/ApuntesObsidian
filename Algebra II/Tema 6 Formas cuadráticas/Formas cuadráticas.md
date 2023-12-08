Dada una matriz $A \in \mathbb{R}^{\text{n x n}}$ simétrica una **forma cuadrática** en $\mathbb{R}^n$ es una función $Q: \mathbb{R}^n \to\mathbb{R}$ tal que: $Q(x) = x^TAx$.

Si $A=\begin{bmatrix}1 & 5 & 0\\ 5 & 4 & 0 \\ 0 & 0 & 2\end{bmatrix}$entonces $Q(x) = x_1^2 + 4x_2^2 + 2x_3^2 + 10x_1x_2$

Si: $Q(x) = x^TAx$, $A\in \mathbb{R}^{\text{3 x 3}}$  simétrica, $Q: \mathbb{R}^3\to\mathbb{R}$, se llama **Superficie de nivel** $k$ al conjunto $S_k = \{x\in \mathbb{R}^3: Q(x) = k, k\in \mathbb{R}\}\subset \mathbb{R}^3$.

## Eliminación de productos cruzados:

Sea $A \in \mathbb{R}^{\text{n x n}}$ simétrica, entonces existe un cambio de variable ortogonal $x = Py$ ($P \in \mathbb{R}^{n \text{ x }n}$ es ortogonal) que transforma la forma cuadrática $Q(x) = x^TAx$ en una forma cuadrática sin productos cruzados, es decir 

                   $Q(x) = \tilde Q(y) = y^TDy = \lambda_1y_1^2 + \lambda_2y_2^2+\dots +\lambda_ny_n^2$,     si $x = Py$

con $D\in \mathbb{R}^{n \text{ x }n}$diagonal. Además, los elementos de la diagonal de $D$ son los autovalores de $A$ y las columnas de la matriz $P$ son autovectores de $A$ y forman una **BON** de $\mathbb{R}^n$. 

Podemos interpretar el cambio de variables geométricamente de la siguiente manera.

Llamemos $u_1$ al primer vector de la **BON** de columnas de una base $B$ que contiene a las columnas de $P$ y $u_2$  al segundo. Entonces si $x \in \mathbb{R}^2$ y $x =Py$ tenemos que

                        $x = Py = \begin{bmatrix}u_1 & u_2\end{bmatrix}\begin{bmatrix}y_1 & y_2\end{bmatrix}^T = y_1u_1+y_2u_2$

con lo cual $y$ no es otra cosa que el vector de coordenadas de $x$ en la base $B$, es decir $y = \big[x\big]^B$

### Clasificación de formas cuadráticas:

Dada una forma cuadrática $Q:\mathbb{R}^n \to \mathbb{R}$ decimos que $Q$ es:

1. Definida positiva si $Q(x) >0 \ \forall x \in \mathbb{R}^n -\{0\}$ .
2. Semidefinida positiva si  $Q(x) \ge 0 \ \forall x \in \mathbb{R}^n$
3. Definida negativa si $Q(x) <0 \ \forall x \in \mathbb{R}^n -\{0\}$ 
4. Semidefinida negativa si $Q(x) \le0 \ \forall x \in \mathbb{R}^n$ 
5. Indefinida si no es ninguna de las anteriores.

**Definición:** Dada una matriz simétrica $A \in \mathbb{R}^{n \text{ x }n}$, decimos que $A$ es definida positiva, semidefinida positiva, etc, si la forma cuadrática asociada $Q(x) = x^TAx$ es, respectivamente, definida positiva, semidefinida positiva, etc.

**Teorema:** Sea $A\in\mathbb{R}^{n\text{ x }n}$ simétrica y sean $\lambda_1,\dots,\lambda_n$ los autovalores de A. Entonces $Q(x) = x^TAx$ es

- d.p. si $\lambda_i > 0$   para todo $i$
- s.d.p. si $\lambda_i \ge 0$ para todo $i$
- d.n. si $\lambda_i < 0$   para todo $i$
- s.d.n. si $\lambda_i \le 0$ para todo $i$
- indefinida si existe un par de índices $i,j$ tales que $\lambda_i >0$ y $\lambda_j < 0$.

### Conjuntos de nivel:

Dada una forma cuadrática $Q: \mathbb{R}^n\to\mathbb{R}$, para $c\in\mathbb{R}$ se define el conjunto de nivel $c$ como

                                                    $N_c(Q) = \{x \in \mathbb{R}^n: Q(x) = c\}$ 

Para determinar que tipo de conjunto es $N_c(Q)$ empleando un cambio de variables $x = Py$ que elimine productos cruzados, tenemos que $Q(x) = \tilde Q(y) = y^TDy$ con $D$ diagonal y que, para un dado $c\in\mathbb{R}$,

                                                           $Q(x) = c \iff \tilde Q(y) = c$

Entonces teniendo en cuenta la interpretación geométrica del cambio de variables, tenemos que el conjunto de nivel $N_c(Q)$ se obtiene rotando adecuadamente el conjunto de nivel $N_c(\tilde Q)$(los ejes $y_i$ se hacen coincidir con las rectas generadas por las columnas de $P$). En particular, ambos conjuntos de nivel tienen la misma forma geométrica.

### Teorema de Rayleigh:

Sea $A \in \mathbb{R}^{n \text{ x }n}$ simétrica y $Q(x) = x^TAx$. Sean $\lambda_M$ y $\lambda_m$ los autovalores máximo y mínimo de A respectivamente, y sean $S_{\lambda_M}$ y $S_{\lambda_m}$ los respectivos autoespacios. Entonces 

1. $\lambda_m\|x^2\| \le Q(x) \le \lambda_M\|x^2\| \ \ \ \forall x \in \mathbb{R}^n$ (Desigualdad de Rayleigh).
2. $\displaystyle \text{máx}_{\|x\| \not= 0} \frac{Q(x)}{\|x\|^2} = \lambda_M$ y el máximo se alcanza en los $x \in S_{\lambda_M}-\{0\}$
3. $\displaystyle \text{min}_{\|x\| \not= 0} \frac{Q(x)}{\|x\|^2} = \lambda_m$ y el mínimo se alcanza en los $x \in S_{\lambda_m}-\{0\}$

En particular, $\text{máx}_{\|x\| = 1} \ Q(x) = \lambda_M$ (resp. $\text{mín}_{\|x\| = 1} \ Q(x) = \lambda_m$)y el máximo (resp. mínimo) se produce en los autovectores unitarios asociados a $\lambda_M$ (resp. $\lambda_m$.