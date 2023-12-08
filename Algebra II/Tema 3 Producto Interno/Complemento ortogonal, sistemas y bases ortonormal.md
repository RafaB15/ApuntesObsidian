Sea $(\Bbb V,\langle.,.\rangle)$ un $\Bbb K$-espacio euclídeo y sea $A \subseteq \Bbb V$ un conjunto no vacío, el complemento o subespacio ortogonal a $A$, denotado por $A^{\bot}$, se define por

                                                     $A^{\bot} :=\{x\in \Bbb V: \langle x,a\rangle=0 \ \ \forall\  a\in A  \}$ 

**Propiedades:**

- $A^{\bot}$  es un subespacio de $\Bbb V$.
- $A\ \cap A^{\bot} = \{0_{_V}\}$.
- Si $B \sube \Bbb V$  es un conjunto no vacío tal que $B \sube A$  entonces $A^{\bot} \sube B^{\bot}$.

**Observación:**

Sea $(\Bbb V,\langle.,.\rangle)$ un $\Bbb K$-espacio euclídeo, $w \in \Bbb V$ y sea $S \sube\Bbb V$ un subespacio de $\Bbb V$ tal que $S=gen\{v_1,v_2,...,v_n\}$. Entonces,

                                      $w \in S^{\bot}$, si y sólo si $\langle w,v_1\rangle=\langle w,v_2\rangle=...=\langle w,v_n\rangle=0$.

Es decir, para ver que $w \in S^{\bot}$ basta ver que $w$ es ortogonal a cada generador de $S$.

### Propiedad:

Sea $(\Bbb V, \langle .,.\rangle)$ un $\Bbb K$-espacio euclídeo de dimensión finita y $S \sube\Bbb V$ un subespacio, entonces:

- $\Bbb V = S \oplus S^{\bot}$
- $\text{dim}(S^{\bot}) + \text{dim}(S) = \text{dim}(\Bbb V)$
- $(S^{\bot})^{\bot} = S$

### **Definición:**

Sea $(\Bbb V,\langle.,.\rangle)$ un $\Bbb K$-espacio euclídeo. Un conjunto de vectores no nulos $\{u_1,u_2,...,u_n\} \sube \Bbb V$ se llama:

- Sistema **ortogonal** cuando

                                                            $\langle u_i,u_j\rangle = 0$  para todo $i \not= j$

- Sistema **ortonormal** cuando

                              $\langle u_i,u_j\rangle = 0$  para todo $i \not= j$ y $\|u_i\| = 1$ para todo $i\in\{1,...,n\}$.

Llamaremos **base ortogonal (ortonormal)** de $\Bbb V$ a los sistemas ortogonales (ortonormales) que generan $\Bbb V$.

Si tengo la base ortogonal $U = \{u_1,u_2,...,u_n\}$ entonces las coordenadas de un vector $x$ en esa base son:

                               $[x]^U = \begin{bmatrix} \langle x,u_1\rangle & \langle x,u_2\rangle & \dots & \langle x,u_n\rangle\end{bmatrix}^T$