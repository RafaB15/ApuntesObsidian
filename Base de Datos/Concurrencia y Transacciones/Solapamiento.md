- Un solapamiento entre dos [[Transacción|transacciones]] $T_1$ y $T_2$ es una lista de $m(T_1) + m(T_2)$ instrucciones en donde cada instrucción de $T_1$ y $T_2$ aparece una única vez y las instrucciones de cada [[Transacción|transacción]] conservan el orden entre ellas dentro del solapamiento. 

- Solapamientos distintos entre dos transacciones:

$$\displaystyle \large \frac{(m(T_1) + m(T_2))!}{m(T_1)!m(T_2)!}$$
# Equivalencia de solapamientos

## Equivalencia de resultados

- Cuando, dado un estado inicial particular, ambos órdenes de ejecución dejan a la base de datos en el mismo estado.
## Equivalencia de conflictos

- Cuando ambos órdenes de ejecución poseen los mismos [[Conflicto|conflictos]] entre instrucciones. 
- Esta noción es particularmente interesante porque no depende del estado inicial de la base de datos. Es la más fuerte de las tres. 
## Equivalencia de vistas

Cuando en cada orden de ejecución, cada lectura $R_{T_i} (X)$ lee el valor escrito por la misma transacción *j*, $W_{T_j} (X)$. Además se pide que en ambos órdenes la última modificación de cada ítem *X* haya sido hecha por la misma transacción.