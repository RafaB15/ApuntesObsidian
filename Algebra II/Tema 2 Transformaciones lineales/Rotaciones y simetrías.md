# Rotación en R2

Para rotar un vector en $R2$ un ángulo $\theta$ en sentido antihorario usamos

                                                          $\displaystyle R(\begin{pmatrix}x_1 \\ x_2\end{pmatrix})= \begin{pmatrix}cos(\theta) & -sen(\theta)\\sen(\theta) &\ \ \  cos(\theta)\end{pmatrix}\begin{pmatrix}x_1 \\ x_2\end{pmatrix}$

Si lo queremos girar en sentido horario usamos $-\theta$ en vez de $\theta$.

# Rotación en R3

### Alrededor del eje z:

                                                         $R_{\theta,z} = \begin{pmatrix}\cos(\theta) & -\sin(\theta) & 0\\\sin(\theta) & \ \ \ \cos(\theta) & 0 \\ 0&0&1\end{pmatrix}$

### Alrededor del eje x:

                                                         $R_{\theta,x} = \begin{pmatrix}1&0&0\\0&\cos(\theta)&-\sin(\theta)\\0&\sin(\theta)&\ \ \ \cos(\theta)\end{pmatrix}$

### Alrededor del eje y:

                                                         $R_{\theta,y} = \begin{pmatrix}\ \ \ \cos(\theta) &0&\sin(\theta)\\0&1&0\\-\sin(\theta)&0&\cos(\theta)\end{pmatrix}$

# Proyectores:

Un proyector es un endomorfismo $\Pi : V \to V$ en cualquier espacio vectorial $V$ que cumple:

                                                                       $\Pi\  \circ\ \Pi = \Pi$

### Observaciones:

- Si $w \in \text{Im}(\Pi) \implies \Pi (w) = w$.
- $\text{Nu}(\Pi)\ \oplus\  \text{Im}(\Pi) = V$

Estas observaciones nos permiten definir una proyección transversal que se nota $\Pi _{S_1S_2}$, Siendo $S_1$ la Imagen de $\Pi$  y $S_2$ el Núcleo de $\Pi$. Se lee la proyección sobre $S_1$  en la dirección de $S_2$.

### Propiedades:

En lo que sigue $V$ es un $K$ espacio vectorial y $S_1$ y $S_2$ subespacios de $V$ tal que $S_1  \oplus S_2=V$ .

1. $\Pi_{S_!S_2} + \Pi_{S_2S_1} = I_{_V}$
2. $\Pi _{S_1 S_2}(v) = v_1$   si   $v=v_1 + v_2, \ \ v_1\in S_1, v_2 \in S_2$
3. $\text{Nu}(\Pi_{S_1 S_2}) = S_2$
4. $\text{Im}(\Pi_{S_1 S_2}) = S_1$
5. $\displaystyle \Pi_{S_1 S_2}(v) = \begin{cases}v & v\in S_1 \\ 0 & v \in S_2\end{cases}$

# Simetría

En lo que sigue $V$ es un $K$ espacio vectorial y $S_1$ y $S_2$ subespacios de $V$ tal que $S_1  \oplus S_2=V$ .

Se define la simetría de $V$ con respecto a $S_1$ en la dirección $S_2$ como la transformación lineal  $\sum_{S_1S_2}:V\to V$ tal que 

                                                    $\sum_{S_1S_2}(v) =\begin{cases}\ \ \ v&v\in S_1\\-v& v \in S_2\end{cases}$

Puede verse que:

                                                    $\sum_{S_1S_2}(v) = v - 2\Pi_{S_1S_2}(v)$

Para comprobar que una transformación lineal es una simietría basta con ver que

                                                         $\sum_{S_1S_2}^2 = I_{_V}$