# Ejercicio1 
## Enunciado

Enumere y justifique qué modelo de concurrencia es más conveniente utilizar para cada no de los siguientes casos de uso

- Calcular productos de matrices para entrenar redes neuronales
- Realizar llamadas a diferentes APIs y combinar sus resultados.
- Procesar los logs de acceso de un sitio web muy concurrido
- Backend de un juego en línea

## Respuesta

- Para los productos de matrices se puede utilizar el modelo fork join, debido a que el calculo de una parte de la matriz final es independiente del cálculo del resto de las partes. Podríamos calcular una o más filas por thread y luego unirlas todas para tener la matriz final. También podés paralelizar las matrices en sí.
	- Podemos también utilizar vectorización. Procesamiento en cpu fuerte, entonces se aplica.
	- No usaría estado mutable compartido porque no hay necesidad de compartir nada.
- Para las llamadas a diferentes apis nos es conveniente un modelo async/await, debido a que son más ligeras que levantar nuevos threads, al usar menos memoria. Multiplexan el uso de hilos del ejecución reales del procesador en varias tareas, para lo que se necesita que esas tareas no estén usando activamente el procesador, tiene que pasar la mayoría del tiempo durmiendo, como lo son operaciones de entrada y salida como llamar a una api. También es más expresivo en el código.
	- También podríamos usar fork join o una barrera de alguna forma.
	- Si usábamos threads y tenemos 3 llamadas de api, podríamos seguir usando threads.

- Para los logs de acceso a un sitio, se pueden procesar con fork join como en el tp.
- Para el backend de un juego en línea / editor colaborativo en línea se usa estado mutable compartido. 

- Por ahí escribir unas pequeñas líneas de código, pero no habrá que codear en papel.