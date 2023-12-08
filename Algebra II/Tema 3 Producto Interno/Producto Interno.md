## Propiedades y definición del producto interno:

Se $\Bbb V$ un $\Bbb K$ espacio vectorial. Un producto interno en $\Bbb V$ es una función $\langle .,.\rangle : \Bbb V \ \text{x} \ \Bbb V \to \Bbb K$, tal que:

i) Para cada $\lambda \in \Bbb K$ y para cada $x,y,z \in \Bbb V$

1. $\langle x+y,z\rangle = \langle x,z\rangle + \langle y, z\rangle$,
2. $\langle \lambda x, y\rangle = \lambda \langle x,y\rangle$.

ii) $\langle x,y\rangle = \overline{\langle y,x\rangle}$, para todo $x,y\in \Bbb V$.

iii) $\langle x,x\rangle > 0$   si $x \not= 0$.

Un  $\Bbb K$ -espacio vectorial con producto interno $\langle .,.\rangle$  se llama espacio euclídeo y lo denotaremos por $(\Bbb V, \langle .,.\rangle )$.

Consecuencias de que $(\Bbb V, \langle .,.\rangle )$ sea un espacio euclídeo:

- $\langle x,\lambda y\rangle = \overline{\langle \lambda y,x\rangle} = \overline{\lambda \langle x,y\rangle} = \overline{\lambda}\langle x,y\rangle$.
- $\langle x,x\rangle \ge 0$ para todo $x \in \Bbb V$  y $\langle x,x\rangle = 0$ si y sólo si $x=0_{_V}$.

## Espacios normados:

Una norma en un $\Bbb K$-espacio vectorial $\Bbb V$ es una función $\|\ .\ \|: \Bbb V \to \Bbb R^+$  , tal que:

i)   $\|x\| = 0$  si y sólo si $x=0_{_V}$.

ii)  $\|\lambda x\| =|\lambda|\ \|x\|$, para todo $x \in \Bbb V$, $\lambda \in \Bbb C$.

iii) $\|x+y\| \le \|x\| + \|y\|$, para todo $x,y\in \Bbb V$ (desigualdad triangular).

El par $(\Bbb V , \| \ . \ \|)$  se llama espacio normado. Si $(\Bbb V , \langle . , .\rangle)$  es un $\Bbb K$-espacio euclídeo, la función 

                                                                 $\boxed{\ \|x\| := \sqrt{ \langle x,x \rangle}\ }$

define una norma en $\Bbb V$. 

**Propiedades:** 

- Sean  $u, v \in \Bbb V$. Entonces

                                                          $\boxed{\ |\ \|u\|-\|v\|\ | \le \|u-v\| \ }$

 

- Sea $(\Bbb V, \langle .,.\rangle )$ un $\Bbb K$-espacio vectorial, $|| \ .\ ||$ la norma inducida por el producto interno y sean $u,v\in \Bbb V$.

                                         $\boxed{\ \|u + v\|^2 = \|u\|^2+\|v\|^2+2Re(\langle u , v\rangle)\ }$

- **Teorema de Pitágoras:** Si $\langle u,v \rangle = 0$ entonces

                                                          $\boxed{\ \|u+v\|^2=\|u\|^2+\|v\|^2 \ }$

- Si $(\Bbb V, \langle .,.\rangle )$ es un $\Bbb R$-espacio euclídeo entonces

                                                     $\boxed{\  4\langle u,v\rangle = \|u+v\|^2 - \|u-v\|^2\ }$

- Si $u,v\in \Bbb V$ la distancia entre $u$ y $v$ se define como

                                                  

                                                       $\boxed{\ d(u,v) = \|u-v\| = \|v-u\|\ }$

[[Operación|Operación *]]

## Matriz de Gram, Gramiano y triángulos

Sea $(\Bbb V, \langle .,.\rangle )$ un $\Bbb K$-espacio euclídeo. Y sea $B=\{v_1,v_2,...,v_n \}$ un conjunto de vectores de $\Bbb V$, se llama la matriz de Gram y se denota por $G_B$ a

                                         $G_B :=\begin{bmatrix}\langle v_1, v_1\rangle & \langle v_1, v_2\rangle & ... &  \langle v_1, v_n\rangle \\  \langle v_2, v_1\rangle &  \langle v_2, v_2\rangle & ... &  \langle v_2, v_n\rangle \\ ... & ... & ... & ... \\  \langle v_n, v_1\rangle &  \langle v_n, v_2\rangle & ... &  \langle v_n, v_n\rangle\end{bmatrix}$

Observar que $G_B \in \Bbb C^{n\text{ x } n}$. Llamaremos Gramiano de $B$ al determinante de $G_B$.

**Teorema:** Si $\Bbb V$ es un espacio de dimensión finita, todo **P.I.** queda definido sobre una base de $\Bbb V$. Más aún si $B=\{v_1, v_2,...,v_n\}$, todo **P.I.** puede escribirse como:

                                                $\langle x,y\rangle = {[x]^B}^T G_B \overline{[y]^B}= {\overline{[y]^B}}^T G_B[x]^B$

Con $G_B \in \Bbb K^{n\text{ x }n}$, matriz hermítica (simétrica) y definida positiva.

                 

                                $\langle u, v\rangle = [x_1,x_2,...,x_n]\begin{bmatrix}\langle v_1, v_1\rangle & \langle v_1, v_2\rangle & ... &  \langle v_1, v_n\rangle \\  \langle v_2, v_1\rangle &  \langle v_2, v_2\rangle & ... &  \langle v_2, v_n\rangle \\ ... & ... & ... & ... \\  \langle v_n, v_1\rangle &  \langle v_n, v_2\rangle & ... &  \langle v_n, v_n\rangle\end{bmatrix}\begin{bmatrix}\overline{y_1} \\ \overline{y_2} \\ ...\\ \overline{y_n}\end{bmatrix}$

Si $B'=\{v'_1,v_2',...,v_n'\}$ es otra base de $\Bbb V$ vale que

                                                         $\displaystyle{G_{B'} = (M_{B'}^B)^T \ G_B\ \overline{M_{B'}^B}}$

donde $\displaystyle{M_{B'}^B}$ es la matriz de cambio de coordenadas de la base $B'$ a $B$.

**Propiedad:** Sea $(\Bbb V, \langle .,.\rangle )$ un $\Bbb K$-espacio vectorial euclídeo de dimensión finita y $\{ x_1,x_2,...,x_n\}$ un conjunto de vectores de $\Bbb V$. Entonces

                               $\{ x_1,x_2,...,x_n\} \text{ es LI si y sólo si } det(G_{\{ x_1,x_2,...,x_n\}}) \not= 0$ 

## Notación para triángulos

Sea $(\Bbb V, \langle .,.\rangle )$ un $\Bbb R$-espacio euclídeo, se define el ángulo $\theta$ entre dos vectores no nulos $x$ e $y$ mediante la fórmula

                                                                    $\displaystyle{\cos\theta :=\frac{\langle x,y\rangle}{\|x\|\ \|y\|} }$

con $\theta \in [0,\pi]$.