Dado un conjunto de funciones $\{\phi_1,\phi_2,..., \phi_n\}$ con $\phi_i \in C^{n-1} (I) \ \forall \ 1 \le i \le n$, se llama **wronskiano $\{\phi_1,\phi_2,..., \phi_n\}$ a**

                    $\displaystyle W(\phi_1,\phi_2,...,\phi_n) = \begin{vmatrix} \phi_1(x_o) & \phi_2(x_o) & ... & \phi_n(x_o) \\ \phi_1'(x_o) & \phi_2'(x_o) & ... & \phi_n'(x_o) \\ \phi_1''(x_o) & \phi_2''(x_o) & ... & \phi_n''(x_o)\\ {.\atop .} \atop . & {.\atop .} \atop . & {.\atop .} \atop . & {.\atop .} \atop . \\ \phi_1^{n-1}(x_o) & \phi_2^{n-1}(x_o) & ... & \phi_n^{n-1}(x_o)\end{vmatrix}$

Si $\{\phi_1,\phi_2,..., \phi_n\} \subset C^{(n-1)} (I)$   y para algún $x_o \in I$ , se cumple $W(\phi_1,\phi_2,...,\phi_n) \not= 0 \implies \{\phi_1,\phi_2,...,\phi_n\}$ es linealmente independiente.

Si $\{\phi_1,\phi_2,..., \phi_n\} \subset C^{(n-1)} (I)$   es un conjunto linealmente dependiente $\implies W(\phi_1,\phi_2,...,\phi_n) = 0 \ \forall x \in I$ .

El recíproco de este teorema no es verdadero. existen funciones tales que $W(\phi_1,\phi_2,...,\phi_n) = 0 \ \forall x \in I$ , pero las funciones no son linealmente dependientes.