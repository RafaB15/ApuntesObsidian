**Definición:** Sea $A \in \mathbb{R}^{m\text{ x }n}$. Una descomposición en valores singulares de A es una factorización 

                                      $A = U\varSigma\  V^T$

con $U \in \mathbb{R}^{m\text{ x }m}$ y $V \in \mathbb{R}^{n \text{ x } n}$ ortogonales y $\varSigma \in R^{m \text{ x } n}$ con

$\displaystyle \varSigma = \begin{bmatrix}D & 0_{r\text{ x }(n-r)} \\ 0_{(m-r)\text{ x }r} & 0_{(m-r)\text{ x }(n-r)} \end{bmatrix}$ y $D = \begin{bmatrix} \sigma_1 & 0 & \dots & 0\\ 0 & \sigma_2 & \dots & 0 \\ \vdots & \vdots & \ddots & \vdots \\ 0 & 0 & \dots & \sigma_r\end{bmatrix}$

con $\sigma_1 \ge \sigma_2 \ge \dots \ge \sigma_r > 0$.

$0_{k\text{ x }l}$ representa la matriz $k \text{ x } l$ cuyos coeficientes son nulos.

**Definición:** Si $A = U\varSigma\  V^T$ es una **DVS** de $A$, a los vectores que aparecen como columnas de la matriz $V$ se los denomina vectores singulares derechos de $A$ mientras que a los que aparecen como columnas de $U$ se los denomina vectores singulares izquierdos de $A$.

**Teorema:** Sea $A \in \mathbb{R}^{m\text{ x }n}$. Entonces existe una descomposición en valores singulares de A.

### Construir una DVS:

Con $A \in \mathbb{R}^{m\text{ x }n}$

1. Calcular los autovalores de $A^TA$ y ordenarlos de mayor a menor: $\lambda_1 \ge \lambda_2\ge\dots\ge\lambda_n$.
2. Hallar una **BON** $\{v_1,\dots,v_n\}$ de $\mathbb{R}^n$ tal que $A^TAv_i = \lambda_iv_i$, $\text{i} = 1,\dots,n$.
3. Calcular las v.s. de $A$, $\sigma_i = \sqrt(\lambda_i)$.
4. Si $r$ es el número de valores singulares de $A$ no nulos, es decir, $\sigma_r > 0$ y $\sigma_i = 0$ para todo $i \ge r + 1$ definir como columnas de $U$

                                     $\displaystyle u_1 = \frac{Av_1}{\sigma_1}, u_2 = \frac{Av_2}{\sigma_2}, \dots , u_r = \frac{Av_r}{\sigma_r}$

1. Si $r < m$, hallar $u_{r+1},\dots,u_m$ tales que $\{u_1,\dots ,u_m \}$ sea **BON** de $\mathbb{R}^m$.
2. Definir las matrices $V = \begin{bmatrix} v_1 & v_2&  \dots & v_n\end{bmatrix}$, $U = \begin{bmatrix} u_1 & u_2&  \dots & u_m\end{bmatrix}$ y 

                       $\displaystyle \varSigma = \begin{bmatrix}D & 0_{r\text{ x }(n-r)} \\ 0_{(m-r)\text{ x }r} & 0_{(m-r)\text{ x }(n-r)} \end{bmatrix}$ y $D = \begin{bmatrix} \sigma_1 & 0 & \dots & 0\\ 0 & \sigma_2 & \dots & 0 \\ \vdots & \vdots & \ddots & \vdots \\ 0 & 0 & \dots & \sigma_r\end{bmatrix}$

1. Entonces $A = U\varSigma\  V^T$ es una **DVS** de $A$.

                          

**Proposición:** Sea $A = U\varSigma\  V^T$ una **DVS** de $A \in R^{m\text{ x }n}$. Entonces 

                                                                     $A^T = V\varSigma^T  U^T$

es **DVS** de $A^T$. En particular $A$ y $A^T$ tienen los mismos valores singulares no nulos.

### Subespacios fundamentales:

Sea $A \in \mathbb{R}^{n \text{ x }m}$ una matriz de rango $r$ y que $A = U\varSigma\  V^T$ es una **DVS** de $A$. Entonces si 

1. $\{v_1,\dots,v_r\}$ es **BON** de $\text{fil}(A)$
2. $\{v_{r+1},\dots,v_n\}$ es **BON** de $\text{Nul}(A)$
3. $\{u_1,\dots,u_r\}$ es **BON** de $\text{col}(A)$
4. $\{u_{r + 1}, \dots , u_m\}$ es **BON** de $\text{Nul}(A^T)$

## DVS reducida:

A partir de una **DVS** de la forma $A = U\varSigma\  V^T$ podemos obtener una descomposición de $A$ que emplea matrices de tamaño reducido. Escribimos $U = \begin{bmatrix} U_r & U_{m-r} \end{bmatrix}$ y $V = \begin{bmatrix} V_r & V_{n-r} \end{bmatrix}$, donde $r$ es el rango de $A$.

Entonces 

            $\displaystyle A = U\varSigma\  V^T = \begin{bmatrix} U_r & U_{m-r} \end{bmatrix}\begin{bmatrix}D & 0_{r\text{ x }(n-r)} \\ 0_{(m-r)\text{ x }r} & 0_{(m-r)\text{ x }(n-r)} \end{bmatrix}\begin{bmatrix} V_r ^T \\ V_{n-r}^T \end{bmatrix} = U_rDV_r^T$

## Matriz seudoinversa de Moore-Penrose:

Sea $A = U_rDV_r^T$ una **DVS** reducida de $A$. La matriz $A^+ = V_rD^{-1}U_r^T$ es la matriz seudoinversa de Moore-Penrose de $A$.

## Solución de cuadrados mínimos de norma mínima:

**Proposición:** Consideremos la ecuación $Ax=b$ con $A \in \mathbb{R}^{m \text{ x }n}$ y $b\in \mathbb{R}^n$. Entonces:

1. Existe una única solución $x^*$ por cuadrados mínimos de la ecuación $Ax = b$ que pertenece a $\text{fil}(A)$.
2. $x^*$ es la única solución por cuadrados mínimos de norma mínima de la ecuación $Ax = b$

**Teorema:** Sea $A \in \mathbb{R}^{m\text{ x }n}$ y sea $A^+$ la matriz seudoinversa de Moore-Penrose de $A$ entonces

1. Para todo $b \in \mathbb{R}^n$, $x^* = A^+b$ es la única solución por c.m. de longitud mínima de la ecuación $Ax = b$.
2. $A^+A = P_{\text{ fil}(A)}$ y $AA^+ = P_{\text{col}(A)}$