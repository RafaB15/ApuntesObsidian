## TO-DOs tecnicos
- [ ] Prueba funcional luego del deploy
	- [ ] armar .features con @not-local (o @notlocal)
	- [ ] correr smoke test, lo hacemos?
	- [ ] agarrar 1/2 escenarios y escribirlos para que corran en forma remota
		- [ ] Deberian verificar cosas contra la base de datos
		- [ ] cargar una peli y leerla
		- [ ] despues de cada deploy verificar alguans cositas que me confirmen que me anda la DB y todo.
- [ ] Cambiar logs a debug
- [ ] Mandar form
- [ ] Mandar mail situación iteración
- [ ] Desloguear api key
- [ ] correcciones de código
	- [ ] contestar comentarios xfa
	- [ ] devolución sobre la arquitectura, cómo mejorarla
- [ ] revisar que los statuses devueltos son correctos y unificar responses, statuses, errores y rescues
- [ ] usar constantes
- [ ] double dispatch?
- [ ] esta bien tirar todo en los controllers? 
- [ ] Como modularizamos el código de los routes? helpers?
- [ ] cambiar el US08 donde no va, esta mal copiado
- [ ] flag para que GET /usuarios no esté disponible en prod/test

## Preguntas técnicas/PO

> [!warning] CONDICIONES PARA APROBAR LA MATERIA (GARANTÍAS)

- `calificar` como request, debería ser un PUT o un POST?
  O PUT para modificar y POST para crear.
- Refactorizamos los gherkin con la modalidad propuesta? Respetamos esto para todos los gherkin? Hay aprox 75 gherkins![[Pasted image 20240612204057.png]]
- Manejo de errores? Calidad del código. Que tanto tiempo y bola le damos?

## Retro iteración 2
- Fail faster. Arrancar a laburar más temprano para iterar los gherkin más rapido.
- Revisar la modalidad de las asignaciones. Proponemos pares cruzados para comunicación y para codeo.
- Laburar en horarios de mañana para favorecer la contestada de mails\
- Alguna mejora para el sistema de comunicación. Demasiados mails. Esto mejoraria laburando antes? O buscamos otra forma?
- *'Consejo: tal vez ANTES de mandarse a cambiar algo, podría ser conveniente consultar si el cambio propuesto está en la dirección correcta.'* - [](https://groups.io/g/fiuba-memo2/topic/106598888#msg684)

## Backlog iteración 3
- #hacer


## Accionables de esta retro:
- [ ] Revisar dinámica de trabajo, trabajar mejor con TDD para rotar más el driver.
	- [ ] meh. Se dificultó el TDD por las malas decisiones de diseño y modelado
	- [ ] De igual manera el equipo rotaba el desarrollo sobre la misma story.
	- [ ] Hubo menos mob y mas pairing.
- [ ] Sesión de programación con un docente para afianzar el tema del desarrollo y el modelado.
	- [ ] No se modeló sobre la API → nuestro principal problema
- [x] Particionar stories de manera que el pivote sea más pequeño a fin de evitar recalculaciones por particionar tarde.
	- [ ] Cumplido.
	- [ ] Problema juli: 
		- [ ] Particionar OMDB en fuevisto/novisto y caso feliz. Requirio un cambio de endpoint para hacer lo de visto. Es 'bloqueante', porque no podemos avanzar con visto si no tenemos el caso feliz.
	- [ ] Problema bruno
		- [ ] Varias particiones no se hicieron en caso feliz y errores que sería lo optimo.
- [ ] Validar con el PO los cambios antes de implementar y presentar.
	- [ ] Sí y no. Validabamos pero al tardar la comunicación comenzabamos igual y una correccion nos generaba un retrabajo.