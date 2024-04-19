# Test Desiderata

- Propiedades deseables que deberían tener los test
- No todos los tests pueden tener las 12 propiedades, dependiendo del contexto una será más deseable que la otra.
- Podemos detectar smells en le diseño de nuestro código a partir de como estamos escribiendo los tests.


- Resumir con sus palabras cada propiedad
- Identificar si se mencionan trade offs
# Comportamiento
- Si cambiamos un número en el código los tests cambian.
- La propiedad es que cuando cambia el comportamiento del código cambia el resultado del test.

# Insensibles a la estructura interna
- La estructura interna del código no tiene que afectar que pase o no un test.
- Probar el comportamiento sin probar el diseño interno.
- Esto nos habilita a hacer refactorizaciones.
# Readable

- Como todo el código, se leeran tests más de lo que se escriben
- Tenemos que pensar en las personas que lo van a leer y tener que entender
- Lo que hace que un código sea bueno es diferente de lo que hace a un test bueno.
- Lo que haríamos para hacer nuestro código más legible suele hacer nuestros tests menos legible.
- En el código se usan constantes.
- Se quiere refactorizar el código.
- Poner constantes en los tests y poner un montón de funciones que setteen el contexto del tests´, o tengan factories los hace menos legibles.
- Es como tener dos líneas de código que use muchas cosas.
- Hay un tradeoff, porque si ponemos constantes entonces solo tenemos que cambiar un lugar para cambiar varios test en caso de refactorizar.
- En los tests es mejor que podamos leerlos directamente de lo que está escrito en los tests en vez de tener que buscar la definición de todo lo que se usa en el test.
- Presenta los datos que se van a usar, la acción y el resultado.

# Writable

- Queremos que los tests sean fáciles de escribir.
- Si tenemos un poco de código que es muy probable que esté bien, pero hacer tests para ese código simple puede tomarnos mucho más tiempo que lo que nos tomó escribirlo.
- Tenemos que pensar en si es algo que queramos testear o no. 
- Si nos toma miles de líneas testear una pequeña función para que llegue a correrla, entonces eso nos dice que hay algo malo con nuestros tests.
- Hay tests en los que tenemos que especificar muchas cosas, algunas que no importan.
- Tenemos que fijarnos, en un test, cuales son las líneas que verdaderamente importan. Si son pocas líneas, entonces eso nos dice que tal vez nuestro código no está bien diseñado y tenemos que abstraer cierta lógica para tener otra interfaz para usarlo.
- Si el test no es fácil de escribir, lo más probable es que tengamos problemas en nuestro código.
- Algunas cosas son muy difíciles de testear y a veces tenemos el trade off de no tenerlo testeado.

# Rápidos

- Los tests deben fallar rápidamente para que uno no pierda el flujo de trabajo.
- Prioriza la latencia antes que la cantidad de tests por segundo que se está corriendo.
- Si setteamos algo al incio y luego corremos los tests con ese set up, convendría tener un set up más corto, que corra algunos test y ver si fallan rápido.

# Determinístico

- Siempre se corre con el mismo input y se tiene la misma salida.
- Si tenés una fecha, hay que pasarle una fecha y no usar la de la compu actual por ejemplo. 
- Hay un trade off porque es más fácil hacer test no determinísiticos pero nos sirven más los determinísticos.
- Hay que evitar los flakey tests, que son los que fallan en muy pocos casos pero como en la amyoría pasan nos olvidamos. Estos no son determinísticos y son un problema.

# Automatizados

- Hay una relación entre automatizar los test y el costo. 
- A largo plazo nos termina beneficiando porque son rápidos para ejecutarlos, pero escribirlos toma mucho más que los tests manuales. Es un trade off.
- Hay que encontrar un balance entre los automáticos y manuales, debido a que los automáticos son una inversión y a veces es muy difícil automatizarlos. Hay que ver cuanto nos cuesta y el payoff de hacerlo.
- Si cambiamos el color de algo, verlo es fácil, testearlo no nos aporta mucho.

# Aislado

- Si cambiamos el orden de los tests, deberían seguir funcionando.
- Si un test cambia un estado global, lo debe resetear cuando termine de ejecutarse.
- Los tests están aislados unos de otros.
- No depende el que pase el test dos de el que pase el test 1.

# Composable

- Funcionalidades entre los test deberían estar aisladas.
- Se prueban las funcionalidades aparte de cada parte y luego algunas combinaciones. No todas las combinaciones, pues ya vimos que por separado funcionan.
- Es deseable pero difícil de hacer.

# Específicos

- Cuando un test falla, tendríamos que saber específicamente donde está el código que falló.
- Los unitarios suelen ser específicos.
- Los tests de aceptación ya no son específicos pero nos sirven. Entonces tenemos un trade off. 

# Predecir el ambiente de producción

- Si los test te dan en verde, entonces cuando pasen al ambiente de producción debería andar todo bien.
- Esto no siempre se cumple pues hay más variables.

# Confianza
- Los tests deben dar confianza de que cuando los tests pasen es porque el programa funciona en verdad.
- Tienen que darle confianza al equipo para seguir avanzando.
- Los test en verde nos deben dar la confianza de desplegar un viernes.

# Test  Doubles
![[Test doubles.png]]
## Mock objects

- Son objetos que solo existen en el ambiente de un test.

## Dummy
- Se pasan por parámetro pero en realidad no se usan. 
- Son para poder probar cierta funcionalidad sin afectar.
- Provee cero funcionalidad o valor. Si se la intenta usar puede incluso dar error. Solo se usa para poder llamar a otra función.
- Un método necesita un parámetro pero el valor del mismo no se usa en la prueba.
- **No es usado por el test/SUT pero es requerido para la creación de algún objeto.**

## Mock object

- Devuelven valores predefinidos y registran llamadas a los métodos.
- Se le pueden definir algunos valores que devuelven algunos de sus métodos. 
- Incluso definir que en la primera llamada de su método devuelva X y en la segunda y. 
- También registra la llamada de sus métodos.
- Se puede registrar con qué valores se llamó a cada método.
- Se suele utilizar mock de manera general, pero los test doubles son de varios tipos.

## Fake Object

- Implementan la lógica e interfaz del objeto que reemplazan.
- En vez de implementar una base de datos SQL entera, implementamos un objeto que solo tiene una lista o diccionario y lo usamos en los tests.

## Spy

- Extra de la clase.
- Se utiliza como el mock pero en general no se le ponen expectativas.
- XUNIT test patterns.

# Paez wisdom

- Complejidad accidental cuando mi código depende de una llamada al sistema operativo (pidiendo la hora por ejemplo).
- Como no nos gusta esa dependencia entonces lo abstraemos, haciendo una clase ProveedorDeFecha por ejemplo, entonces nuestro código ya no depende de eso únicamente.
- En ciclo chico generamos el mock dinámicamente, en el grande lo hacemos en la variable de ambiente.
- Ahora se usa debug en vez de byebug.