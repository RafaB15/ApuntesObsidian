
# Consigna

Usar el comando “dig" con las opciones iterativa, autorizada y verborrágica capturando por la pantalla de la terminal y también mediante "Wireshark". 
Subirlo al Campus un informe en formato PDF.

# Resolución

Se decidió utilizar la url de youtube, la cual es *www.youtube.com*

Al ejecutar el comando ``dig www.youtube.com`` sin ninguna flag, el resultado es el siguiente.

![[Pasted image 20240331204313.png]]

Podemos ver que en la **ANSWER SECTION** nos devuelve múltiples direcciones ip para youtube.com, seguramente debido a que balancean la carga.

Podemos notar también que una de las respuestas que nos da es del tipo **CNAME** (canonical name), con lo cual parece que **www.youtube.com** es un alias para **youtube-ui.l.google.com.**

En Wireshark podemos ver los paquetes de pregunta y respuesta

![[Pasted image 20240331210145.png]]

![[Pasted image 20240331210152.png]]

Si además agregamos la flag `+trace`, entonces no solamente nos devolverá los resultados del servidor DNS autoritario, sino que también nos devolverá los resultados de todos los servidores en el medio.

![[Pasted image 20240331213054.png]]
![[Pasted image 20240331213111.png]]

Por parte de Wireshark, podemos apreciar como se hicieron muchos más pedidos a servidores DNS en muy poco tiempo, como podemos apreciar por el atributo time.

![[Pasted image 20240331213241.png]]

