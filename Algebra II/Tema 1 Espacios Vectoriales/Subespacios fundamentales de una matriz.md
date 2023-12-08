Dada $A \in K^{m \ x \ n}$ se definen los subespacios:

- $Col(A) = gen\{col_1(A), col_2(A), ...,col_n(A)\} \subset K^m$.
- $Fil(A) = gen\{fil_1(A), fil_2(A), ...,fil_m(A)\} \subset K^n$.
- $nul(A) =\{ x\in K^n/Ax=0_{_{K^m}}\} \subset K^n$.
- $nul(A^T) =\{ x\in K^m/A^Tx=0_{_{K^n}}\} \subset K^m$.

Se define **rango columna** de una matriz a la cantidad de columnas l.i. que tiene una matriz.

Se define **rango fila** de una matriz a la cantidad de filas l.i. que tiene una matriz.

Se prueba que $\forall A\in K^{m\ x\ n}$  **rango columna(A) = rango fila(A)**, por lo tanto hablamos directamente de **rango(A) = n° de filas l.i de A = n° de columnas l.i de A = rg(A).**

- Propiedades de las dimensiones y los rangos
    
    $\text{Fil(A) = Col(A}^T)$
    
    $**\text{dim(Fil(A)) = dim(Col(A))}**$
    
    $**\text{dim(Col(A)) + dim(Nul(A)) = dim(}K^n)**$
    
    $**\text{dim(Fil(A)) + dim(Nul(A}^T\text{)) = dim(}K^m)**$
    
    $\text{ragno(A) + dim(Nul(A)) = n (número de columnas de A)}$
    
    $\text{ragno(A) + dim(Nul(A}^T\text{)) = m (número de filas de A)}$
    

### Recordar:

- El sistema $\text{Ax = b}$ tiene solución si y solo si $b \in Col(A)$.
    - Si la solución es única  $\iff$las columnas de A constituyen un conjunto linealmente independiente $\iff$$Nul (A) = \{0_{_{K^n}}\}$.
    - Si la solución no es única  $\iff$las columnas de A constituyen un conjunto linealmente dependiente$\iff$$Nul (A) \not= \{0_{_{K^n}}\}$.
- Si $x_p$ es cualquier solución particular del sistema de ecuaciones lineales $\text{Ax = b}$ de modo que $\text{A}x_p = \text{b}$ y $x_h$ es solución del sistema homogéneo asociado $\text{Ax = 0}_{K^m}$. Es decir $\text{A}x_h\text{ = 0}_{K^m}$entonces todas las soluciones del sistema se expresan como $x = x_p + x_h$.
- Cuando buscamos el **espacio columna** de una matriz miramos las columnas pivotales, volvemos a la primer matriz y tomamos las columnas que **originalmente** ocupaban las posiciones de tales columnas pivotales.
- Cuando buscamos el **espacio filas** de una matriz, la reducimos y nos quedamos simplemente con una  base dada por aquellas filas que no se anularon, pero estas filas que no se anularon las sacamos de la matriz **ya reducida**