Una matriz $A \in \Bbb K^{\text{n x n}}$ con espectro $\sigma(A) = \{\lambda_1,\lambda_2,\dots,\lambda_m\}$ es diagonalizable si y sólo si existen matrices $\{G_1, G_2, \dots, G_m\}$ tales que

 **(1)**                                         **$A = \lambda_1 G_1+\lambda_2G_2+\dots + \lambda_mG_m$**

donde las $G_i$ tienen las siguientes propiedades

- $G_i$ es la proyección sobre $\text{nul}(A-\lambda_iI)$ en la dirección de $\text{col}(A - \lambda_iI)$.
- $G_iG_j = 0$ para $i \not= j$.
- $G_1 + G_2 + ... + G_m = I$.

El desarrollo **(1)** se denomina la descomposición espectral de $A$ y las $G_i$ se llamas los proyectores espectrales asociados.

## Ejemplo:

![[Algebra II/Tema 4 Autovalores y autovectores/Teorema espectral para matrices diagonalizables/Untitled.png|Untitled]]

![[Algebra II/Tema 4 Autovalores y autovectores/Teorema espectral para matrices diagonalizables/Untitled 1.png|Untitled]]

Cuando hacemos que $A=P\ Q\ P^{-1}$. Si llamamos $X$ a las columnas de $P$ y $Y$ a las filas de $P^{-1}$, entonces

                                                         $G_i = X_iY_i$