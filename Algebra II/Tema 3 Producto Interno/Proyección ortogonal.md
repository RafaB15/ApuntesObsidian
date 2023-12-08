Sea $(\Bbb V, \langle .,.\rangle)$ un $\Bbb K$-espacio euclídeo, $S \sube\Bbb V$ un subespacio de dimensión finita y $v\in \Bbb V$, decimos que $\hat{v}$ es la proyección ortogonal del vector $v$ sobre el subespacio $S$ si verifica:

- $\hat v \in S$
- $v- \hat v \in S^{\bot}$

Más aún, si $B_S=\{v_1,v_2,...,v_n\}$ es una base ortogonal de $S$ entonces:

                                      $\displaystyle \hat v = \frac{\langle v,v_1 \rangle}{\|v_1\|^2} v_1 + \frac{\langle v,v_2 \rangle}{\|v_2\|^2} v_2 + \dots+ \frac{\langle v,v_n \rangle}{\|v_n\|^2} v_n$ 

Con esto podemos definir una función $P_S: \Bbb V\to \Bbb V$ como la función que a cada elemento $v \in \Bbb V$ le asigna su proyección ortogonal sobre $S$, es decir

                          $\displaystyle P_S(v):=\hat v = \frac{\langle v,v_1 \rangle}{\|v_1\|^2} v_1 + \frac{\langle v,v_2 \rangle}{\|v_2\|^2} v_2 + \dots+ \frac{\langle v,v_n \rangle}{\|v_n\|^2} v_n$ 

$P_S$ es una transformación lineal que cumple:

- $P_S^2 = P_S$, es decir $P_S$ es un proyector.
- $\text{Im}(P_S) = S$ y $\text{Nu}(P_S) = S^{\bot}$. Entonces, claramente $\Bbb V = \text{Im}(P_S) \oplus \text{Nu}(P_S)$ y además $\text{Im}(P_S) \ \bot \ \text{Nu}(P_S)$.
- Como $P_S$ es un proyector y tenemos que $\text{Im}(P_S) = S$ y $\text{Nu}(P_S) = S^{\bot}$ entonces

                                                          $P_{S^{\bot}} = I_{\Bbb V} - P_S$

## Matriz de la proyección ortogonal:

Si $\Bbb V$ es dimensión finita y $B$  es cualquier base de $\Bbb V$, podemos calcular la matriz de la transformación lineal $P_S$ en dicha base $B$. 

Si $B=\{w_1,w_2,\dots,w_n\}$ es una base del espacio vectorial $\Bbb V$ entonces, las columnas de $[P_S]^B_B$  nos quedan

                       $[P_S]^B_B = \begin{bmatrix}[P_S(w_1)]^B & [P_S(w_2)]^B & \dots & [P_S(w_n)]^B\end{bmatrix} \in \Bbb K^{n\text{ x }n}$

## Otro método para calcular proyección ortogonal

$\Bbb S$ es un subespacio no trivial de un espacio euclídeo $(\Bbb V, \langle .,.\rangle)$

$P_S(v)$ proyección ortogonal de $v$ sobre $\Bbb V$, $B = \{w_1,w_2,\dots ,w_n \}$ base de $\Bbb V$.

Las coordenadas de la proyección respecto de la base $B$, $\begin{bmatrix}x_1 & x_2 &\dots & x_n \end{bmatrix}^T$

               $\begin{bmatrix}\langle w_1, w_1\rangle&\langle w_1, w_2\rangle  & \dots &\langle w_1, w_n\rangle \\ \langle w_2, w_1\rangle & \langle w_2, w_2\rangle & \dots & \langle w_2, w_n\rangle \\ \vdots & \vdots & \dots & \vdots \\ \langle w_n, w_1\rangle  & \langle w_n, w_2\rangle & \dots & \langle w_n, w_n\rangle\end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \\ \vdots \\ x_n \end{bmatrix} = \begin{bmatrix}\langle v, w_1\rangle \\ \langle v, w_2\rangle \\ \vdots \\ \langle v, w_n\rangle \end{bmatrix}$