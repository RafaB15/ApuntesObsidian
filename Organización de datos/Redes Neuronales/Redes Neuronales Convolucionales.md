# Filtros

Tal vez nos interese cambiar algunas de estas funciones intermedias, según la aplicación que le queramos dar.

![[Organización de datos/Redes Neuronales/Redes Neuronales Convolucionales/Untitled.png|Untitled]]

Podríamos usar funciones (o *filtros*) especiales para este caso.

Una función podría ser una convolución de imágenes.

Y otra podría ser una función de max-pooling.

Un filtro es simplemente una convolución de una zona de la imagen.

![[Organización de datos/Redes Neuronales/Redes Neuronales Convolucionales/Untitled 1.png|Untitled]]

Hiper parámetros a definir:

- Cantidad de filtros a usar.
- Tamaño del filtro (ej 3x3).
- Stride (paso)
- Padding

Los parámetros son los coeficientes del filtro y eso lo aprende la red!

## Max-Pooling

En maxpooling, para secciones de la imagen se obtiene la ***feature*** más importante. Es otra manera de obtener información local.

![[Organización de datos/Redes Neuronales/Redes Neuronales Convolucionales/Untitled 2.png|Untitled]]

# Convolutional neural network

La red quedaría de esta manera:

![[Organización de datos/Redes Neuronales/Redes Neuronales Convolucionales/Untitled 3.png|Untitled]]

![[Organización de datos/Redes Neuronales/Redes Neuronales Convolucionales/Untitled 4.png|Untitled]]

## Resultados

![[Organización de datos/Redes Neuronales/Redes Neuronales Convolucionales/Untitled 5.png|Untitled]]

# Conv1d (Convolucionando Texto)

Es posible aplicar el mismo concepto que usamos para imágenes en textos.

Para eso en primer lugar tenemos que representar a cada palabra del texto como un vector de “n” dimensiones mediante un embedding.

Word2vec, GloVe son formas populares de crear embeddings o podemos usar embeddings ya creados para un determinado idioma.

![[Organización de datos/Redes Neuronales/Redes Neuronales Convolucionales/Untitled 6.png|Untitled]]