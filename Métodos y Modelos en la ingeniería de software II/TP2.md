- Consummidor externo como postman puede consultar nuestra web api
- El telegram bot también se comunica con la web api. Es un process daemon que está siempre pegándole a telegram y consultando is tiene información nueva.
- Web api
	- Ruby con padrino
	- API Rest (no devuelve .htmls como jobvacancy)
	- Comunicación con base de datos
	- Repo base nos dan.
- Telegram Bot
	- Daemon
	- Telegram le envía los mensajes que le escriben
	- Capa de presentación de nuestra aplicación.
		- NO entender que el bot haga todo.
		- Hay que separar en capas
		- Hay que construir el bot de la misma forma que construimos la api
		- No podremos correr gherkin automatizados
		- Igual habrá que poner un gherkin.
		- En el bot se arma el mensaje con la información que responde la api

- Para la web api, la vamos a subir a render exactamente en job vacancy.
- Para el telegram bot, lo tendremos en kubernetes.
- Sumologic se va a utilizar para los logs. Se comunica con ambos, la web api en render y telegram en kubernetes. Es un agregador de logs.

![[Pasted image 20240516082144.png]]