- Es el principal protocolo de la [[Application Layer|capa de aplicación]] para sistemas de mail electrónico en internet.
- Utiliza la transferencia de datos confiable de [[Transmission Control Protocol|TCP]] para transferir mail del servidor de mail del remitente al servidor de mail del destinatario.
- Los **user agents** vendrían a ser los clientes como Outloook o Apple Mail que nos dejan mandar y leer mails. Al querer mandar un mail, este se manda al mail server del remitente, desde donde se manda al mail server del destinatario.

![[SMTP.png]]

- SMTP tiene dos lados, el lado del cliente, que se ejecuta en el mail server del remitente, y el lado del servidor, que se ejecuta en el mail server del destinatario.
- Entonces en cada mail server se puede correr tanto el lado del cliente como de servidor.

![[SMTP in action.png]]![[SMTP with protocols.png]]