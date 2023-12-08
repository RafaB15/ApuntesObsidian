# Hipótesis distribucional

La hipótesis asume que la semántica de una palabra está determinada por el contexto en el que aparece.

- Hoy fuí en auto al trabajo.
- Hoy fuí en subte al trabajo.
- Me tomé el subte
- Me tomé el colectivo.

Esto implica que podríamos obtener el significado de las palabras si las resumimos en todos lo contextos en los cuales aparecen.

## Word2Vec:

Nos propone construir, por medio de la hipótesis distribucional, vectores para cada palabra. Representar cada palabra como un vector.

Empezamos con un embedding al azar y con un hiperparámetro “windows” entrenamos de distintas formas

![[Organización de datos/NLP II/Representaciones vectoriales Word2vec, Tasttexr y/Untitled.png|Untitled]]

![[Organización de datos/NLP II/Representaciones vectoriales Word2vec, Tasttexr y/Untitled 1.png|Untitled]]

![[Organización de datos/NLP II/Representaciones vectoriales Word2vec, Tasttexr y/Untitled 2.png|Untitled]]

Entreno cada palabra para que esté más “cerca” de cuyo.

### Resultados

![[Organización de datos/NLP II/Representaciones vectoriales Word2vec, Tasttexr y/Untitled 3.png|Untitled]]

 

### Uso

Dada una palabra vamos a tener si significado.

Dado un texto podemos dividirlo en palabras y después pasarlo a vectores.

***Ejemplo: “Hola, ¿Cómo estás?”***

Puede ser tokenizado en:

![[Organización de datos/NLP II/Representaciones vectoriales Word2vec, Tasttexr y/Untitled 4.png|Untitled]]

***Ejemplo:***

Clasificación de noticias por tema (policial, internacional, etc) nos sirve más convoluciones pooling.

Detección de sentimientos: RNN

Moderador de malas palabras: Convoluciones, pooling de ciertos grupos de palabras

 

### Problema de word2vec: Palbras desconocidas

¿Qué hacemos con las palabras que no entraron en nuestro vocabulario, y por lo tanto, son desconocidas?

La solución de word2vec es entrenar un vector especial “desconocido” para cada palabra que se encuentre y no esté en su vocabulario.

Esto no es ideal ya que se desaprovecha información de la palabra, por ejemplo “Gianmarkistan” no está en ningún vocabulario, pero probablemente haga referencia a un lugar.

# Fasttext

![[Organización de datos/NLP II/Representaciones vectoriales Word2vec, Tasttexr y/Untitled 5.png|Untitled]]

Aparición de una palabra desconocida

![[Organización de datos/NLP II/Representaciones vectoriales Word2vec, Tasttexr y/Untitled 6.png|Untitled]]

Si tenemos suerte esta suma va a relacionar la palabra con “sal” y va a quedar cerca del vector de “sal” (ya que comparte muchos n-gramas). El terminar con “ar” le agrega una cercanía con los verbos.

# Char embeddings

Supongamos que aparece la palabra “sala” y no está en nuestro vocabulario.

![[Organización de datos/NLP II/Representaciones vectoriales Word2vec, Tasttexr y/Untitled 7.png|Untitled]]

![[Organización de datos/NLP II/Representaciones vectoriales Word2vec, Tasttexr y/Untitled 8.png|Untitled]]

![[Organización de datos/NLP II/Representaciones vectoriales Word2vec, Tasttexr y/Untitled 9.png|Untitled]]

![[Organización de datos/NLP II/Representaciones vectoriales Word2vec, Tasttexr y/Untitled 10.png|Untitled]]

# Transformers

Los transformers introducidos en el paper “Attention is all you need” son arquitecturas que pueden leer secuencias y devolver secuencias pero más rápido que las RNNs y con mejores resultados y una posibilidad de retener conocimiento por una longitud arbitraria.

Modelos famosos como BERT y GPT3 funcionan gracias a estas capas.

# Conclusiones

- Podemos crear vectores que contengan el significado de las palabras.
- Con los vectores de palabras y redes neuronales recurrentes o convolucionales podemos extraer significado de los textos.
- Según lso tipos de textos y lo que queramos predecir vamos a elegir la arquitectura.
- Para lidiar con palabras desconocidas podemos utilizar Fasttext o char embeddings.
- Los transformes se usan en el estado del arte de las tareas de NLP.