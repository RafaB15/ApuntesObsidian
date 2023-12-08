## Matriz ortogonal (unitaria):

Se dice que una matriz $U \in \Bbb R^{\text{n x n}}$ es **ortogonal** si 

                                                            $U^{-1} = U^{T}\iff U U^T = \text{I}_n$

                          

- **Propiedades teniendo una matriz U ortogonal**
    - Las columnas de $U$ forman una **base ortonormal** de $C^n$.
        
        En general, si $U = [u_1|u_2|\dots|u_n]$ entonces
        
                                                          $\langle u_i,u_j \rangle = \begin{cases} 1 \text{ si } j = i  \\ 0 \text{ si } j \not= i\end{cases}$
        
    - Las filas de $U$ forman una **base ortonormal** de $C^n$.
    - $\langle Ux, Uy \rangle = \langle x,y \rangle\  \forall x,y \in \Bbb C^n$ .
        
        Se suele decir que $U$ "conserva" el **P.I.**
        
        Por lo tanto: $\|Ux\| = \|x\| \ \forall x\in\Bbb C^n$. 
        
    - Si $\lambda$ es autovalor de $U$ $\implies |\lambda| = 1$.
    - $|\text{det}(U)| = 1$.
    - Cuando la matriz de una transformación lineal es ortogonal, esta es una isometría, se conserva el módulo.

## Matriz hermítica:

Se dice que una matriz $A \in \Bbb C^{\text{n x n}}$ es **hermítica** si 

                                                              $A = \overline A^{T} = A^*$

- **Resultados importantes sobre matrices hermíticas.**
    
    Si $A \in \Bbb C^{\text{n x n}}$ es una matriz hermítica, se cumple:
    
    - $\langle x, Ay \rangle = \langle Ax, y \rangle$
    - $\overline x^TAx \in \Bbb R$
    - Si $\lambda$  es autovalor de $A \implies \lambda \in R$.
    - Si $v_1$ es autovector de $A$ asociado a $\lambda_1$ y $v_2$ es autovector de $A$ asociado a $\lambda_2$, $\lambda_2 \not= \lambda_1 \implies v_1 \bot v_2$.

## Matriz simétrica (también es hermítica):

Se dice que una matriz $A \in \Bbb R^{\text{n x n}}$ es **simétrica** si

       

                                                                       $A = A^T$

- **Resultado importante de matrices simétricas**
    
    $A \in \Bbb R^{\text{n x n}}$ simétrica $\iff$existen matrices $P \in \Bbb R^{\text{n x n}}$ ortogonal y $D = \text{diag}(\lambda_1,\dots,\lambda_n) \in \Bbb R^{\text{n x n}}$, tal que $A = P\ D\ P^T$.
    
    Es equivalente a decir:
    
    $A \in \Bbb R^{\text{n x n}}$ simétrica $\iff$existe una base ortogonal de $\Bbb R^n$ formada por autovectores de $A$. (Por lo tanto, existe una **BON** de $\Bbb R^n$ formada por autovectores de A).
    

## Matriz Normal:

Se dice que una matriz $A \in \Bbb C^{\text{n x n}}$ es **normal** si 

                                       

                                                             $AA^*=A^*A$

Las matrices normales son semejantes unitariamente a una matriz diagonal en $\Bbb C^{\text{n x n}}$.

## Relación entre las matrices $A$ y $A^{*}$

- $\langle x,Ay \rangle = \langle A^{*}x,y \rangle$
- $\text{Nul}(A^{*}) = (\text{Col}(A))^{\bot}$
- $\text{Nul}(A) = (\text{Col}(A^{*}))^{\bot}$
- n $\text{Col}(A^{*}) = (\text{Nul}(A))^{\bot}$
- $\text{Col}(A) = (\text{Nul}(A^{*}))^{\bot}$