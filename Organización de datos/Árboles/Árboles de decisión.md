- Árbol con ramas para cada valor en la comparación.
- En cada nodo dividimos el set de datos de acuerdo a un cierto criterio.
- Son árboles donde cada rama evalúa algún dato para definir por qué rama continúa ese dato. En cada nodo hacemos una división del set de datos en base a algún criterio.
- Objetivo: llegar a nodos hoja en los cuales podamos clasificar correctamente nuestros datos.
- Algoritmos:
    - ID3
    - C4.5
    - C5.0
    - CART

# Ventajas:

- Simples de entender e interpretar: modelo de caja blanca.
- Funcionan con datos numéricos o categóricos.
- Requieren poca preparación de los datos: no requieren normalización.
- Buena performance para datasets grandes.
- Ayudan en la selección de features.

# Limitaciones:

- Encontrar el óptimo es NP-complete.
    - Algoritmos greedy para encontrar óptimos locales.
- Árboles demasiado complejos generan overfitting.
    - Poda

# Algoritmos:

## ID3:

- 1979
- Algoritmo tipo greedy:
    - En cada paso realiza el mejor split posible en dos.
    - Selecciona el atributo que nos da mayor Ganancia de información (relación con la entropía, el atributo con la menor entropía).
- Esto se repite recursivamente hasta construir el árbol final.
- Features deben ser categóricos, no acepta atributos numéricos.

### Ejemplo:

![[Organización de datos/Árboles/Árboles de decisión/Untitled.png|Untitled]]

- Primero calculamos la entropía del set de datos

![[Organización de datos/Árboles/Árboles de decisión/Untitled 1.png|Untitled]]

$$
H[\frac{5}{8};\frac{3}{8}] = 0.9544
$$

Recordamos que la entropía la calculamos como menos la sumatoria de las probabilidades por los logaritmos en base dos de las probabilidades.

$$
-\sum_{i=1}^nP_i * \log_2P_i
$$

- Atributo: ***Presencia***:
    
    ![[Organización de datos/Árboles/Árboles de decisión/Untitled 2.png|Untitled]]
    
    H(Presencia = buena) = H[4/4; 0/4] = 0  → 4 tienen categoría sí y 0 tienen categoría no
    
    H(Presencia = maña) = H[0/2; 2/2] = 0
    
    H(Presencia = regular) = H[1/2; 1/2] = 1
    
    H(Presencia) = 4/8 * 0 + 2/8 * 0 + 2/8 * 1 = 0.25 → Para sacar la entropía del atributo presencia sumamos el producto de la probabilidad de cada atributo por su entropía.
    
    GI(Presencial) = 0.9544 - 0.25 = 0.7044 →Ganancia de información
    
- Atributo: ***Estudios:***

![[Organización de datos/Árboles/Árboles de decisión/Untitled 3.png|Untitled]]

![[Organización de datos/Árboles/Árboles de decisión/Untitled 4.png|Untitled]]

- Atributo: ***Experiencia:***

![[Organización de datos/Árboles/Árboles de decisión/Untitled 5.png|Untitled]]

- Como el atributo que tiene menor entropía y, por ende, mayor ganancia de información es ***Presencia***  entonces hacemos el split en base a este. Los datos que tienen la clase Buena terminan en un nodo hoja porque todos corresponden a una misma clase (Si), lo mismo para loa clase Mala (con No). Para la clase regular nos quedan valores con Si y con No, por lo que tendremos que seguir haciendo splits.

![[Organización de datos/Árboles/Árboles de decisión/Untitled 6.png|Untitled]]

![[Organización de datos/Árboles/Árboles de decisión/Untitled 7.png|Untitled]]

- ID3 tiene las características:
    - Gran peligro de Overfitting.
        - Realizar preguntas hasta que todas las hojas tengas nodos de una sola clase.
    - Uso del hiper-parámetro minbucket para reducir el riesgo de overfitting.
        - Indica la cantidad mínima de registros que puede tener un nodo no hajo.
    - Hojas del árbol indican la probabilidad de cada clase en base a cuantos registros de cada clase hay en el nodo hoja.

## C4.5:

- Sucesor de ID3.
- Acepta atributos numéricos.
- Acepta datos con atributos faltantes.
- Los atributos pueden tener un peso.
- Poda del árbol.

![[Organización de datos/Árboles/Árboles de decisión/Untitled 8.png|Untitled]]

- Primero ordena los valores y luego hace el split probando diferentes puntos en donde hacerlo hasta encontrar el que tenga la mayor ganancia de información para este atributo. En este caso dividir por 27 nos da mayor ganancia.

![[Organización de datos/Árboles/Árboles de decisión/Untitled 9.png|Untitled]]