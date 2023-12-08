$\displaystyle\boxed{\text{Si }S_1,S_2\subset V \text{son subespacios de } V \implies S_1 \cap S_2\text{ es un subespacio}}$

El subespacio $S_1 \cap S_2$ es el mayor subespacio contenido simultáneamente en los subespacios $S_1$ y $S_2$.

Si $S_1$ y $S_2$  son subespacios de un espacio vectorial $V$, se llama suma de $S_1$ y $S_2$ al conjunto:

$\displaystyle \boxed{S_1 + S_2 =\{v \in V / v=s_1 + s_2, \text{ con }s_1\in S_1 \text{ y }s_2\in S_2\}}$

- **Observaciones**
    - $S_1 + S_2$ es un subespacio.
    - Se dice que es el menor subespacio que incluye a $S_1 \cup S_2$.
    - Si $S_1 = gen\{v_1,...,v_k\}$ y $S_2 = gen\{w_1,...,w_m\}\implies S_1 +S_2 =gen\{v_1,...,v_k,w_1,...,w_m\}$
    - $(S_1 \cup S_2) \subset (S_1 + S_2)$
    - Todo subespacio que contiene a $S_1 \cup S_2$ incluye también a $S_1 + S_2$
    - $dim(S_1+S_2)=dim(S_1)+dim(S_2) - dim(S_1 \cap S_2)$

Se dice que la suma de $S_1$  y $S_2$ es **directa,** o que $S_1$ y $S_2$ están en suma directa si para cada $v \in S_1+ S_2$ existen únicos $s_1 \in S_1$ y $s_2 \in S_2$ tal que $v = s_1 + s_2.$ Cuando la suma es directa se nota $S_1 \oplus S_2$.

$**\boxed{S_1\text{ y }S_2 \text{ están en suma directa si y sólo si }S_1 \cap S_2 = \{0_{_V}\}}$** 

Dado un subespacio $S \subset V$, $K$ espacio vectorial, se dice que $W$ es un suplemento de $S$ si     $S \oplus W = V$.