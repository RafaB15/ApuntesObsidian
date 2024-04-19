- Conjunto de programas secuenciales que pueden ejecutarse en paralelo. Con el scheduler se pueden ejecutar por turnos en un mismo procesador o en varios y hacerlo al mismo tiempo.

# Desafíos

- Necesidad de sincronizar y comunicar procesos diferentes.
- **Sincronización**: Coordinación temporal entre distintos procesos.
- **Comunicación**: Datos que necesitan compartir los procesos para cumplir la función del programa.
- **Programa concurrente**: Consiste en un conjunto finito de procesos secuenciales.
- **Procesos**: Están compuestos por un conjunto finito de instrucciones atómicas.
- **Ejecución del programa concurrente:** Resulta al ejecutar una secuencia de [[Instrucción Atómica|instrucciones atómicas]] que se obtiene de intercalar arbitrariamente las instrucciones atómicas de los procesos que lo componen.

# Modelos de Concurrencia:

- [[Estado Mutable Compartido]]
- [[Paralelismo fork-join]]
- Canales / mensajes
- [[Programación asincrónica]]
- Actores.