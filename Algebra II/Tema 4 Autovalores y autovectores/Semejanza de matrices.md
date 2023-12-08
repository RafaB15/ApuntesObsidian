## Definición:

Sean $A$  y $B$ dos matrices en $\Bbb K^{\text{n x n}}$, se dice que $B$ es **semejante** a $A$ si existe $Q \in K^{\text{n x n}}$ inversible, tal que $B = Q\ A\ Q^{-1}$.

Se nota $B \sim A$.

- **Consideraciones**
    - Las matices diagonalizables son matrices semejantes a una matriz diagonal.
    - La relación de semejanza es reflexiva, $A \sim A$ pues $A= \text{I}\  A\  \text{I}$ y también simétrica pues $B \sim A \iff \exists Q$  tal que $B = Q\ A\ Q^{-1} \iff Q^{-1}\ B=A \implies A\sim B$.
    - La relación de semejanza es transitiva.
    
           Si $B \sim A$ y $C \sim B \implies C \sim A$.
    
    - Si $\Bbb V$ es un espacio vectorial de dimensión $n$ y  $B$ y $B'$ son bases de $\Bbb V$, para toda t.l. $T: \Bbb V \to \Bbb V$ se cumple que $\displaystyle [T]^{B'}_{B'} = M_B^{B'}[T]_B^BM_{B'}^{B} = M^{B'}_B[T]_B^B(M_B^{B'})^{-1}$.
    
          Todas las representaciones matriciales de $T$ con respecto a una misma base son semejantes 
    
          entre sí.
    

### Propiedad importante:

Si $B \sim A \implies A$ y $B$ tienen los mismos autovalores con la misma multiplicidad algebraica y geométrica.