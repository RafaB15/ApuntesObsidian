- Las pruebas de verificación son pruebas técnicas para  controlar que hayamos construido el producto tal como pretendimos construirlo. 
- Son pruebas que los propios desarrolladores ejecutan para ver que están logrando que el programa funcione como ellos pretenden.
- Se compone de:
	- **Pruebas unitarias (Unit testing)**: Verifican pequeñas porciones de código. Por ejemplo, verifican alguna responsabilidad única de un método.
	- **Pruebas de integración (Integration testing)**: Prueban que varias porciones de código, trabajando en conjunto, hacen lo que pretendíamos. Por ejemplo, se trata de pruebas que involucran varios métodos, clases o incluso subsistemas enteros.
	- **Pruebas de regresión (Regression testing)**: Garantizan que la aplicación siga funcionando correctamente después de producirse algún cambio en el código.
	- **Pruebas de punta a punta (E2E o End-to-End testing)**: Verifican funcionalidades que atraviesan todas las capas de la aplicación, p. ej. desde la pantalla a la base de datos.
	- **Pruebas de sistema (System testing)**: Evalúan cómo los diferentes componentes interactúan juntos en la aplicación completa e integrada
- Hay ocasiones en que debemos probar código que necesita de otros objetos, métodos o funciones para poder funcionar: en esas situaciones se utilizan objetos ficticios o dobles de prueba (stubs, mocks, fakes, etc.), que ayudan a aislar el código a probar. 
- Las pruebas de verificación podrían ser de caja negra o de caja blanca:
	- **Caja negra:** Cuando la ejecutamos sin mirar el código que estamos probando. 
	- **Caja blanca**: Cuando analizamos el código durante la prueba.
- En general, se prefiere probar el funcionamiento y no verificar la calidad del código.