# Parte 1:

- [x]  Realizar 6 visualizaciones que ayuden a entender o explicar el target.

Todas las visus cumplen:

- [x]  Debe explicarse por si misma, sin necesidad de texto aclaratorio.
- [x]  Debe tener rótulos en los ejes que corresponda y en el título.
- [x]  Debe mostrar una relación o algo con la variable pedida que sea claro e interesante.
- [x]  El uso de color debe ser intencional, elegido por ustedes, no por la librería.
- [x]  La visualización debe ser legible (por ejemplo, un bar plot de 40 barras es ilegible)

# Parte 2:

- [x]  Utilizar todas las columnas del dataset con encoding donde sea necesario.
- [x]  Utilizar búsqueda de hiperparámetros.
- [x]  Reproducibilidad garantizada.
- [x]  Contestar ¿Cuál es el mejor score de validación obtenido? (¿Cómo conviene obtener el dataset para validar?)
- [x]  Contestar Al predecir con este modelo para test, ¿Cúal es el score obtenido? (guardar el csv con predicciones para entregarlo después)
- [x]  ¿Qué features son los más importantes para predecir con el mejor modelo? Graficar.

No hace los siguientes:

- [x]  Utiliza mal los datos de validación ya sea para obtener el resultado o para buscar hiper parámetros (-4 puntos), ejemplos: calcular el score con otras labels, el set de validación se usa para elegir los parámetros pero también está dentro del entrenamiento de cada modelo, el set de validación se usa filtrando información a los encodings, validación no está tomado de forma correcta, etc.
- [x]  El modelo no está bien hecho (-4 puntos), ejemplo: entrenan con las labels o datos cambiados para algunas filas
- [x]  No es capaz de predecir para test o no lo hace correctamente (-4 puntos)
- [x]  No es reproducible (-2 puntos)
- [x]  No obtiene bien los features más importantes (-2 puntos)
- [x]  La predicción en test da menos de 0,3 (-2 puntos)
- [x]  La predicción para test tiene errores (-1 punto)
- [x]  No utiliza todas las columnas del dataset (-1 punto)

# Parte 3:

- [x]  Entrenar un Random Forest
- [x]  Entrenar un XGBoost
- [x]  Busqueda de hiperparámetros para cada uno
- [x]  Deben utilizar top-2 accuracy como métrica de validación.
- [x]  Deben medirse solo en validación, **no contra test!!!**
- [x]  Deben ser reproducibles (correr el notebook varias veces no afecta al resultado).
- [x]  Deben tener un score en validación superior a 0,3.
- [x]  Para el feature engineering debe utilizarse imputación de nulos, mean encoding y one hot encoding al menos una vez cada uno.
- [x]  Deben utilizar al menos 40 features (contando cómo features columnas con números, pueden venir varios de la misma variable).
- [x]  Deben utilizar CountVectorizer o TfIdfVectorizer para algunos features.
- [x]  Deberán contestar la siguiente pregunta: Para **el mejor modelo de ambos**, ¿cuál es el score en test? (guardar el csv con predicciones para entregarlo después)

No hacer

- [x]  Para cada modelo cada condición no cumplida (o mal hecha) resta 1 punto.
- [x]  Feature engineering inapropiado para el modelo elegido (-2 puntos), ejemplos: features que no están normalizadas para una red neuronal, features sin ninguna consideración de escalas para un KNN, etc.
- [x]  No buscan para todos los hiperparametros importantes (-2 puntos).