Si $\Bbb V$ y $\Bbb W$  son espacios vectoriales de dimension finita, podemos encontrar una expresion matriarcial para una transformacion lineal $T: V \to  W$.

Supongamos que $B$ y $B'$ son bases de $\Bbb V$ y $\Bbb W$ respectivamente. $B = \{v_1, \cdots, v_n\}, B' = \{w_1, \cdots, w_m\}$

$$
x \in \Bbb V,\quad x = \alpha_1 v_1 + \cdots + \alpha_n v_n \implies T(x) = T(\alpha_1 v_1 + \cdots + \alpha_n v_n)

\\\,\\

\Big[T(x)\Big]^{B'} = \alpha_1\big[T(v_1)\big]^{B'} + \cdots + \alpha_n\big[T(v_n)\big]^{B'}
$$

$$
\Big[T(x)\Big]^{B'} = 
\underbrace{\Big[ \big[T(v_1)\big]^{B'} \big| \cdots \big| \big[T(v_n)\big]^{B'}\Big]}_{\text{Matriz de la transformación lineal}}
\begin{bmatrix}\alpha_1 \\ \vdots \\ \alpha_n\end{bmatrix}
$$

Si $B = \{v_1,...,v_n\}$ base de $V, B'=\{w_1,...,w_n\}$ base de $W$ y $T: V\to W$ t.l. la matriz $[\ [T(v_1)]^{B'} |...| \ [T(v_n)]^{B'}] \in K^{\text{mxn}}$, se llama la matriz de $T$ con respecto a las bases $B$ y $B'$ y se nota: $[T]_B^{B'}$, es la única matriz que cumple:

                                                               $[T(x)]^{B'} = [T]_B^{B'}[x]^B$

Siendo $[T]_B^{B'}$ la matriz de la transformación lineal.

### Observaciones:

- Las columnas de $[T]_B^{B'}$ son las coordenadas de los generadores de la $\text{Im}(T)$, por lo tanto $\text{rg}([T]_B^{B'}) = \text{dim(Im(}T))$.
- $x \in \text{Nu(}T) \iff [T]_B^{B'}[x]^B = 0_{_{K^m}}$.
- $\text{Nul(}[T]_B^{B'})$ es el subespacio de las **coordenadas de los vectores de $V$ que están en el $\text{Nu} (T)$.**
- $w \in \text{Im}(T) \iff \exists \ \ x \in V$  tal que $T(x) = w \iff [T(x)]^{B'}=[w]^{B'} \iff [T]_B^{B'}[x]^B = [w]^{B'}$.
- Si $G: W\to U$   es t.l. y $B''$ es base de $U$, entonces se cumple: $[G\circ T]_B^{B'} = [G]_{B'}^{B''}[T]_B^{B'}$.
- Si $T$  es un isomorfismo, $[T]_B^{B'} \in K^{n \ \text{x} \ m}$ y es inversible.
- Se cumple $[T^{-1}]_{B'}^B = ([T]_B^{B'})^{-1}$.
- $\displaystyle [T]^A_D = M^A_B \ [T]^B_C \ M_D^C$