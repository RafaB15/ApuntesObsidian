Dada la matriz $A \in \mathbb{R}^{\text{m x n}}$, la matriz $A^TA$ es simétrica y semidefinida positiva. 

**Definición:** Sea $A \in \mathbb{R}^{\text{m x n}}$. Sean $\lambda_1, \lambda_2,\dots,\lambda_n$ los autovalores de $A^TA$ ordenados en forma decreciente, es decir,

                                $\lambda_1 \ge \lambda_2\ge\dots\ge\lambda_n\ge 0$

Entonces $\sigma_i = \sqrt(\lambda_i)$ es el i-ésimo valor singular de $A$.

**Proposición:** Sea $A \in \mathbb{R}^{\text{m x n}}$. Entonces si $\sigma_1$ y $\sigma_n$ son, respectivamente, el mayor y el menor valor singular de $A$, se tiene que

                         $\underbrace{\text{máx}}_{\|x\| = 1}\|Ax\| = \sigma_1$         y             $\underbrace{\text{mín}}_{\|x\| = 1}\|Ax\| = \sigma_n$

**Teorema:** Sea $A\in \mathbb{R}^{m\text{ x }n}$. Supongamos que $\lambda_1, \lambda_2,\dots,\lambda_n$ son los autovalores de $A^TA$ y que 

                        $\lambda_1 \ge \lambda_2\ge\dots\ge\lambda_r \ge \lambda_{r+1} = \dots = \lambda_n =  0$

en otras palabras, los autovalores de $A^TA$ están ordenados en forma decreciente y el número de autovalores no nulos es $r$.

Sea $\{v_1,\dots, v_n\}$ una **BON** de $\mathbb{R}^n$ tal que $A^TAv_i=\lambda_iv_i$.

Entonces

1. $\{Av_1,\dots,Av_n\}$ es un conjunto ortogonal y $\|Av_i\|=\sqrt(\lambda_i) = \sigma_i$ para todo $i = 1,\dots,n$
2. $\displaystyle\{\frac{Av_1}{\sigma_1},\dots,\frac{Av_r}{\sigma_r}\}$ es **BON** de $\text{col}(A)$
3. $\{v_{r+1},\dots, v_n\}$ es **BON** de $\text{Nul}(A)$
4. $\text{rango}(A) = r =$  número de valores singulares no nulos de $A$

## Valores singulares

Si $A \in \Bbb C^{\text{m x n}}$ se dice que $\sigma$ es un **valor singular** de $A$ si $\sigma = \sqrt{\lambda}$,

con $\lambda$ autovalor de $A^TA$.

Si $\lambda_1, \lambda_2,\dots,\lambda_n$, son los autovalores de $A^TA$ ordenados en forma decreciente $\lambda_1 \ge \lambda_2\ge\dots\ge\lambda_k\ge 0$ entonces $\sigma_i = \sqrt{\lambda_i}$ es el i-ésimo valor singular de $A$.

Por las observaciones anteriores, si $\text{rg}(A)=k$, podemos ordenar los valores singulares de A de mayor a menor: 

$\sigma_1 \ge \sigma_2\ge\dots\ge\sigma_k>0$ y $\sigma_{k+1} =\dots=\sigma_n=0$

### Subespacios fundamentales

Entonces, $\forall A\in \Bbb C^{\text{m x n}}$ con $rg(A) = k$, al construir la base ortonormal de $\Bbb C^n$, $B = \{v_1,\dots, v_k,v_{k+1},\dots,v_n\}$, formada por autovectores de $\overline{A}^TA$ asociados a $\lambda_1 \ge \lambda_2\ge\dots\ge\lambda_k> 0, \lambda_{k+1} = \dots = \lambda_n$.

Hemos encontrado bases ortonormales de 3 de los 4 espacios fundamentales de la matriz $A$:

- $\{v_1,\dots, v_k\}$ **BON** de $\text{Fil}(A)$ en $C^n$.
- $\{v_{k+1},\dots, v_n\}$ **BON** de $\text{Nul}(A)$ en $\Bbb C^n$.
- $\displaystyle\{\frac{Av_1}{\sigma_1},\dots,\frac{Av_k}{\sigma_k}\}$ **BON** de $\text{Col}(A)$ en $\Bbb C^m$.

También tenemos que

$\|AV_i\|= \sqrt{\lambda_i} = \sigma_i \ \forall i=1,2,\dots,n$

## Descomposición en Valores Singulares de A

La matriz $A \in \Bbb C^{\text{m x n}}$ se puede factorizar $A=U\varSigma V^T$ en donde $U \in \Bbb C^{\text{m x m}}$ y $V \in \Bbb C^{\text{n x m}}$ son ortogonales y $\varSigma \in \Bbb C^{\text{m x n}}$ con

           $\varSigma = \begin{bmatrix}\varSigma_r & 0_{rx(n-r)} \\ 0_{(m-r)xr} & 0_(m-r)x(n-r) \end{bmatrix}$ y $\varSigma_r = \begin{bmatrix} \sigma_1 & 0 & \dots & 0\\ 0 & \sigma_2 & \dots & 0 \\ \vdots & \vdots & \ddots & \vdots \\ 0 & 0 & \dots & \sigma_k\end{bmatrix}$                                    

$\sigma_1 \ge \sigma_2 \ge \dots \ge \sigma_k$

- Para hallar la matriz ortogonal $V$ hallamos una base ortonormal $\{v_1,\dots, v_n\}$ de $\mathbb{R}^n$ tal que $A^TAv_i = \lambda_i v_i$

                            $V=\begin{bmatrix} v_1 & v_2 & \dots & v_n \end{bmatrix}$

- Para hallar la matriz ortogonal $U$ usamos que $u_i = \frac{Av_i}{\sigma_i}$ , $1 \le i \le r$ y en el caso que $k < m$ se completa a una base ortonormal de $\mathbb{R}^m$ se tiene entonces

                             $U=\begin{bmatrix} u_1 & u_2 & \dots & u_m \end{bmatrix}$

## Descomposición en valores singulares reducida