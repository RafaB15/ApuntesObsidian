Si $U$ es ortonormal entonces

- $U$ preserva longitudes: $\|Ux\|=\|x\|$ para todo $x \in \Bbb R^n$.
- $U$ preserva el producto escalar: $\langle Ux,Uy \rangle = \langle x,y \rangle$ para todo $x,y \in \Bbb R^n$.

## Isometría:

Si $U \in \Bbb R^{\text{n x n}}$ es una matriz ortogonal, entonces la transformación lineal $T$ definida por $T(x) = Ux$ preserva las distancias y los ángulos entre vectores.

## Lo que usaremos mucho:

Recordemos que una matriz cumple lo siguiente con sus autovalores y autovectores:

                                                                    $AV = \lambda V$

Por lo cual, si un autovalor es 1, A multiplicada por el subespacio asociado a este autovalor estará fija, mientras que si un autovalor es -1, entonces A multiplicado por el subespacio de este se irá al otro lado del eje de simetría.  

# Caracterización de matrices ortogonales de 2 x 2:

Sea la matriz ortogonal $U \in \Bbb R^{\text{2 x 2}}$

### Caso 1:

Si $\text{det}(U)=1$ entonces estamos ante una rotación de la forma

                                                                  $U = \begin{bmatrix} \cos\theta & -\sin \theta  \\\sin \theta & \ \ \ \cos\theta \end{bmatrix}$

Geométricamente se trata de una rotación de ángulo $\theta$ en sentido antihorario.

### Caso 2:

Si $\text{det}(U) = -1$ entonces estamos ante una simetría de la forma.

                                                                  $U = \begin{bmatrix} \cos\theta & \ \ \ \ \sin \theta  \\\sin \theta &  -\cos\theta \end{bmatrix}$

y  es semejante a 

                                                                   $U \sim \begin{bmatrix} 1 & \ \ \ 0 \\ 0 & -1 \end{bmatrix}$

Geométricamente se trata de una simetría ortogonal en la dirección de $B$ con respecto a $A$, siendo estos

                                          $A = \text{gen} \{\begin{bmatrix} \cos (\theta/2) \\ \sin(\theta/2)\end{bmatrix}\}$       $B = \text{gen} \{\begin{bmatrix} -\sin (\theta/2) \\ \ \ \ \  \cos(\theta/2)\end{bmatrix}\}$

En otras palabras, es una simetría ortogonal en la dirección del autoespacio asociado al autovalor -1 con respecto al autoespacio asociado al autovalor 1. 

# Caracterización de matrices ortogonales de 3 x 3:

Sea la matriz ortogonal $U \in \Bbb R^{\text{3 x 3}}$.  Como polinomio característico debe tener al menos una raíz real, tiene que haber al menos un -1 o un 1 en el espectro de $U$.

Recordemos que $\mu(x) = y$ es una función a la que si le introducimos una raíz nos dice su multiplicidad algebraica.

## Caso 1:

Si $\text{det}(U)=1$, $U$ es una rotación de ángulo $\theta$  en sentido antihorario.

                                                       $U \sim \begin{bmatrix} 1 & 0 & 0 \\ 0 & \cos\theta & -\sin\theta \\ 0 & \sin\theta &\ \ \ \ \cos\theta \end{bmatrix}$

$U$ tiene a 1 como autovalor simple, $\mu(1) = 1$. Por lo que el eje de rotación será el autoespacio generado por el autovector de 1.

                                                     $UV=V \to gen\{V\}$ es el eje de rotación

También podremos crear una base ortonormal de $R^3$

                                                                 $B = \{V, W_1,W_2\}$

generando $W_1$ y $W_2$ el subespacio ortonormal a V.

## Caso 2:

Si $\text{det}(U)=-1$, entonces tendremos dos casos dependiendo de la multiplicidad del autovalor 1.

Si $\mu(1) = 2$, $U$ es una simetría ortogonal, diagonalizable y semejante a la matriz

                                                            $U \sim\begin{bmatrix} -1 & 0 &  0 \\ \ \ \ 0 & 1 & 0 \\ \ \ \ 0 & 0 & 1 \end{bmatrix}$ 

Geométricamente,  esto significa que $U$ es la simetría ortogonal con respecto al plano $\text{nul}(U - I)$ en la dirección $\text{nul}(U + I)$.

                                                                         $AV=-V$

                                                                       $AW_1 = W_1$

                                                                       $AW_2 = W_2$

Simetría con respecto al plano $gen\{W_1,W_2\}$ en la dirección de $V$.

Si $\mu(1) = 0$, entonces $\mu(-1) = 1$. En este caso $\text{nul}(U+I) = gen\{v_1\}$ para algún $v_1$ de norma 1. Extenderemos $\{v_1\}$ a una base ortonormal de $\mathbb{R}^3 \{v_1,v_2,v_3\}$ tal que $v_3 = v_1\  \text{x} \ v_2$. Entonces podemos deducir que la matriz de isometría $T(x) = Ux$ con respecto a la base $B=\{v_1,v_2,v_3\}$ es semejante a

                $U \sim \begin{bmatrix} -1 & 0 & 0 \\ \ \ \ 0 & \cos\theta & -\sin\theta \\ \ \ \ 0 & \sin\theta &\ \ \ \ \cos\theta \end{bmatrix} = \begin{bmatrix} -1 & 0 &  0 \\ \ \ \ 0 & 1 &  0 \\ \ \ \ 0 & 0 & 1 \end{bmatrix}\begin{bmatrix} 1 & 0 & 0 \\ 0 & \cos\theta & -\sin\theta \\ 0 & \sin\theta &\ \ \ \ \cos\theta \end{bmatrix}$

Geométricamente, esto significa que $U$ es una rotación de ángulo $\theta$  en sentido antihorario alrededor del eje generado por el vector $v_1$ seguida de una simetría ortogonal con respecto al complemento ortogonal del eje de rotación (plano $gen\{V_2,V_3\}$)

### Método para encontrar en ángulo de rotación:

Supongamos que $U \in R^{3 \text{ x }3}$ es una matriz ortogonal tal que $\text{det}(U)=1$. Sabemos que $U$ es una rotación de ángulo $\theta$ en sentido antihorario alrededor del eje $\text{nul}(U-I)$. Para encontrar el ángulo de rotación seguimos los siguientes pasos:

1. Hallar $v_1 \in \text{nul}(U-I)$ tal que $\|v_1\| = 1$. Este vector genera el eje de rotación.
2. Hallar $v_2$ tal que $\|v_2\| = 1$ y $v_2 \ \bot\  v_1$.
3. Hallar $\theta \in (0,2\pi)$ tal que

                               $1 + 2\cos(\theta) = \text{tr}(U)$          y          $\sin(\theta) = \text{det}(\begin{bmatrix} v_1 & v_2 & Uv_2 \end{bmatrix})$

Nota: En la ecuación del seno lo que más nos preocupa es su signo, pues poniendo eso junto al coseno podemos saber exactamente en qué ángulo gira.