# Consultas de MongoDB

## Ejercicio 1

### Enunciado

Obtener los ids, cantidad de hashtags y likes para tweets que tengan 50 o más likes (‘favorite count’) y hayan sido a las 3 de la tarde. 
Ordenar la salida de forma descendente por cantidad de likes. Utilice una única consulta básica con ``find(, ).sort({}).limit({})``.

### Resolución

```
db.tweets.find(
		{
			favorite_count: {$gte: 50},
			"created_at.date": /T15:00:00/
    },
  	{	
			_id: 1,
			hashtags: {$size: "$entities.hashtags"},
			favorite_count: 1,
		}
)
```

## Ejercicio 2

### Enunciado

Para cada hashtag obtener los usuarios que lo utilizaron además del máximo, mínimo y promedio de retweets, sólo teniendo en cuenta aquellos tweets que utilicen más de 3 hashtags (primero se deben filtrar los tweets y luego hallar los valores por cada hashtag). Se debe utilizar el pipeline de agregación.

### Resolución

```
db.tweets.aggregate([
  {
    $match:
      {
        $expr: {$gte: 
			[
		        {$size: "$entities.hashtags"}, 
		        3
	        ]},
      },
  },
  {
    $unwind:
      "$entities.hashtags",
  },
  {
    $project:
      {
        _id: 0,
        hashtag: "$entities.hashtags.text",
        usuario: "$user.id_str",
        retweets: "$retweet_count",
      },
  },
  {
    $group:
      {
        _id: "$hashtag",
        max_retweets: {
          $max: "$retweets",
        },
        min_retweets: {
          $min: "$retweets",
        },
        avg_retweets: {
          $avg: "$retweets",
        },
        usuarios: {
          $push: "$usuario",
        }
      }
  }
])
```

## Ejercicio 3

### Enunciado

Dada la consulta, explicar qué sucede en cada paso del pipeline y en forma resumida qué resuelve la query completa.

![[Parcialito 6 ej 1, 3.png]]

### Resolución

Este pipeline tiene distintas etapas:
-  `match`: Nos quedamos con los objetos que cumplen que 
	- Su idioma es español o portugués.
	- Se hicieron desde Brasil.
- `group`: 
	- Primero se agrupa en base al parámetro in_reply_to_status_id_str y, en caso de que este sea nulo, se toma como si el valor fuera el del id asignado por mongo.
	- Se crea un campo llamado *tweets* con el comando push, que tendrá una lista con objetos con los campos tweet_id, text, user y created_at.
	- Se hace un arreglo llamado languages que tendrá un set con las diferentes cantidades de retweets.
- `project`:
	- tweet va a ser el resultado de arrayElemAt, que recibe un array y un index y devuelve el elemento en el index. El index que se le pasa es cero y el array que se le pasa es el generado por filter. El filtro se va a quedar solo con los tweets que tengan el mismo tweet id que id.
	- replies va a ser un array en el que tendremos una lista con todos los tweets que no estén en la lista de tweets, ordenados por su fecha de creación.
	- Parece que terminamos con dos listas, una de tweets normales y la otra de respuestas.
	- También se selecciona el avg_retweet para mostrar.

# Consultas de Neo4j

## Ejercicio 1

### Enunciado

Investigue los crímenes cometidos en 165 Laurel Street, muestre las personas que participaron de algún crimen y si tienen relación entre ellas muéstrela.

### Resolución

Haciendo la siguiente consulta vemos que hay cinco crímenes que sucedieron en la locación

```cypher
MATCH 
	(c:Crime) - [:OCCURRED_AT] ->(l:Location) 
WHERE 
	l.address = "165 Laurel Street" 
RETURN c,l
```

![[Crimines.png]]

Para ver a las personas involucradas en estos hechos, hacemos la siguientes consulta

```cypher
MATCH 
	(c:Crime) -[:OCCURRED_AT]->(l:Location), 
	(p:Person)-[:PARTY_TO] - (c) 
WHERE 
	l.address = "165 Laurel Street" 
RETURN c,l,p
```

![[Pasted image 20231118224441.png]]

Vemos que dos de los crímenes que sucedieron en esta ubicación involucran cada uno a una persona. Además, estas personas a su vez son familiares.

## Ejercicio 2

### Enunciado

Muestre la (o las) persona(s) que ha(n) realizado mas de 7 comunicaciones telefónicas.

### Resolución

Obtenemos a las personas que han realizado más de 7 comunicaciones telefónicas a través de la siguiente consulta

```cypher
MATCH
    llamada = (t:Phone) -- (c:PhoneCall),
    (p:Person) - [:HAS_PHONE] - (t)
WITH p, COUNT(llamada) AS llamadas
WHERE llamadas > 7 RETURN p
```

![[Pasted image 20231118233343.png]]

Tenemos entonces 30 personas que han sido parte de más de 7 llamadas telefónicas.