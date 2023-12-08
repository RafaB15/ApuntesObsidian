- Dado un [[Serializabilidad#Solapamiento|orden de ejecución]], un conflicto es un par de instrucciones $(I_1, I_2)$ ejecutadas por dos [[Transacción|transacciones]] distintas $T_i$ y $T_j$ , tales que $I_2$ se encuentra más tarde que $I_1$ en el orden, y que responde a alguno de los siguientes esquemas: 
	- $(R_{T_i} (X), W_{T_j} (X))$: Una transacción escribe un ítem que otra leyó. 
	- $(W_{T_i} (X), R_{T_j} (X))$: Una transacción lee un ítem que otra escribió. 
	- $(W_{T_i} (X), W_{T_j} (X))$: Dos transacciones escriben un mismo ítem. 
- En otras palabras, tenemos un conflicto cuando dos transacciones distintas ejecutan instrucciones sobre un mismo ítem *X*, y al menos una de las dos instrucciones es una escritura. 
- Todo par de instrucciones consecutivas $(I_1, I_2)$ de un [[Solapamiento|solapamiento]] que no constituye un conflicto puede ser invertido en su ejecución (es decir, reemplazado por el par ($I_2, I_1$)) obteniendo un solapamiento equivalente por conflictos al inicial.