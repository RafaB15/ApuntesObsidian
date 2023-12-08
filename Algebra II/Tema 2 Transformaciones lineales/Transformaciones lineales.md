Sea $V_{_K}$ y $W_{_K}$ dos espacios vectoriales definidos sobre el mismo cuerpo de escalares $K$.

La función $T:V_{_K} \to W_{_K}$ es una transformación lineal si y sólo si cumple:

1. $T(x+y)=T(x) + T(y), \forall x,y \in V_{_K}$
2. $T(\alpha x) = \alpha T(x), \forall \alpha \in K, \forall x \in V_{_K}$ 

Si $V$ y $W$ son dos $K$ espacios vectoriales y $T: V \to W$ es una transformación lineal:

- Se dice que $V$ es el dominio de $T$ y $W$ el codominio de $T$.
- La imagen de $T$ es el conjunto:  $\text{Im}(T) = \{w\in W \text{ tal que, }v \in V, T(v) = w\}$
- Si $S \subset V, S \not= \emptyset,$  se llama imagen de $S$ por $T$, al conjunto: $T(S) = \{ w \in W: \exists\ x \in S, w=T(x)\} \subset W$
- Si $U \subset W, U \not= \emptyset$ se llama Preimagen de $U$ por $T$, al conjunto: $T^{-1}(U)=\{x \in V: T(x) \in U\} \subset V$.
- Se llama **Núcleo** de $T$ al conjunto: $\text{Nu} (T) = \{ x \in V: T(x) = 0w\} = T^{-1}(\{ 0_{_W}\}) \subset V$.

### Observaciones:

- $T: V\to W \implies T(0_{_V}) = 0_{_W}$
- Si $V = gen\{v_1,v_2,...,v_m\} \implies \text{Im}(T) = gen\{T(v_1),...,T(v_m)\}$
- Si $S$ es subespacio de $V$ $\implies T(S)$ es subespacio de $W$.
- Si $U$ es subespacio de $W$ $\implies T^{-1}(U)$ es subespacio de V.
- Toda t.l. queda univocamente determinada sobre una base.

### Teorema de la dimensión:

                                             $\text{dim(Nu(T)) + dim(Im(T)) = dim(V)}$

### Clasificación de transformaciones lineales:

- Se dice que $T$ es **monomorfismo** si es una transformación lineal inyectiva.
    
    $F:V \to W$  es inyectiva si $x_1 \not= x_2 \implies F(x_1) \not= F(x_2).$  Esto es equivalente a decir que $F$ es inyectiva si $F(x_1) = F(x_2) \implies x_1 = x_2$ .
    
- Se dice que $T$ es **epimorfismo** si es una transformación lineal suryectiva.
    
    $F:V \to W$  es suryectiva si $Im(F) = Cod(F) = W$.
    
- Se dice que $T$ es **isomorfismo** si es una transformación lineal biyectiva.
    
    $F: V \to W$  es biyectiva si es inyectiva y suryectiva.
    

Si $T$ es un isomorfismo entonces existe la función inversa $T^{-1}$.

$T(v) = w_{_0} \begin{cases} \text{si }w_{_0} \notin \text{Im}(T) & \text{el sistema es incompatible.} \\ \text{si } w_{_0} \in \text{Im}(T)\text{ y } T \text{ es monomorfismo} & \text{la ecuación tiene solución única}\\\text{si }w_{_0} \in \text{Im}(T) \text{ y } T \text{no es monomorfismo} & \text{la ecuación tiene infinitas soluciones} \\ \text{Todas las soluciones son de la forma} & x_p + x_N; x_N \in \text{Nu}(T) \text{ y } x_p \text{ solución particular.} \end{cases}$