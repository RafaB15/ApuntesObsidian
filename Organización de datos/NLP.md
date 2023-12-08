Significa Natural Language Processing, a veces se dice PLN, procesamiento de lenguaje natural.

Es una intersección entre la computación, la lingüistica y la inteligencia artificial, cuyo objetivo es que las máquinas comprendan el lenguaje humano.

## Tokenizado de textos

Esto es agarrar un texto y dividirlo ciertas unidades de significado.

![[Organización de datos/NLP/Untitled.png|Untitled]]

## Bag Of Words (BOW)

Es tomar las palabras más comunes y crear un vector para cada uno de los documentos en nuestra base de datos. En este pone 1 si la palabra está y cero si no (no se cuentan varias veces las apariciones de palabras).

![[Organización de datos/NLP/Untitled 1.png|Untitled]]

Si se hace una búsqueda o query calculamos el coseno entre esta y los vectores de las páginas.

![[Organización de datos/NLP/Untitled 2.png|Untitled]]

![[Organización de datos/NLP/Untitled 3.png|Untitled]]

## Term Frequency ( Count Vectorizer)

Es bastante parecido a Bag Of Words, pero en este se cuentan todas las apariciones de una palabra

![[Organización de datos/NLP/Untitled 4.png|Untitled]]

![[Organización de datos/NLP/Untitled 5.png|Untitled]]

![[Organización de datos/NLP/Untitled 6.png|Untitled]]

![[Organización de datos/NLP/Untitled 7.png|Untitled]]

## TF-IDF: Term Frequency x Inverse Document Frequency

El IDF se calcula por cada palabra

$$
\text{IDF(palabra)} = \log{\frac{N + 1}{\text{frecuencia}}}
$$

N: Cantidad total de documentos

frecuencia: la cantidad de **documentos** en los que aparece *palabra*

Este va a dar muy alto si la palabra no aparece en muchos documentos y muy bajo si aparece en muchos documentos.

Entonces calculamos los IDF de todas las palabras.

![[Organización de datos/NLP/Untitled 8.png|Untitled]]

Luego los multiplicamos en la tabla con la cantidad de veces que aparecen en cada documento

![[Organización de datos/NLP/Untitled 9.png|Untitled]]

![[Organización de datos/NLP/Untitled 10.png|Untitled]]

![[Organización de datos/NLP/Untitled 11.png|Untitled]]

![[Organización de datos/NLP/Untitled 12.png|Untitled]]

## Normalización

Podemos querer que distintas palabras vayan al mismo token.

- comer, comemos, comeré: comer
- auto, automóvil, automotriz: auto
- solo, soledad, solitario: solo

## Stemming

Es un proceso en donde se elimina la última parte de las palabras por algún proceso (hay stemmers de varios tipos). El objetivo es llegar a la raíz (stem) de la palabra por medio de su prefijo. Ejemplos:

- caballo, caballería → caball
- biblioteca, bibliotecario → bibliotec
- canto, canta, cantamos, cantan → cant
- cantidad, cantidades →cant

## Lemmatization

Devuelve la base de la palabra (lemma), muchas veces por medio de un diccionario de lemmas para cada palabra.

Ejemplos:

- caballo, caballería → caballo
- biblioteca, bibliotecario →biblioteca
- canto, canta, cantamos, cantan → canto
- cantidad, cantidades → cantidad

## Stopwords

Las stopwords o “palabras vacías” son palabras demasiado comunes o sin significado como artículos, pronombres, preposiciones, etc.

A veces (por ejemplo usando BOW o TF-IDF) queremos removerlas.