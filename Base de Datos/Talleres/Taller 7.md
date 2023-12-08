# Consultas Básicas

1. Hallar los tweets del usuario con userid ‘818839458’.

```
db.tweets.find({_id: "1143929112639279104"})
```

2. Hallar aquellos tweets que tengan más de 500000 retweets.

```
db.tweets.find({retweet_count: {$gt: 500000}}, {_id: 1, retweet_count: 1})
```

3. Mostrar la cantidad de retweets de los tweets que se hayan hecho desde Argentina o Brasil.

```
db.tweets.find({ $or: [{"user.location": "Argentina"}, {"user.location": "Brasil"}]}, {retweet_count: 1})
```

```
db.tweets.find({"user.location": /(argentina|brazil)/i}, {retweet_count: 1})
```

- El `/(argentina|brazil)/i` es una expresión regular para búsqueda sin importar si los caracteres están en mayúscula o minúscula.

4. Hallar los usuarios que tengan tweets con 200000 o más retweets y sean en idioma español.

```
db.tweets.find({retweet_count: {$gte: 200000}, lang: "es"}, {_id: 1, user: 1})
```

5. Mostrar la cantidad de retweets para los tweets que no se hayan hecho en Argentina ni Brasil, pero sí tengan un lugar definido y sean en español.

```
db.tweets.find({lang: "es", "user.location": {$nin: ["Argentina", "Brasil"]}, "user.location": {$ne: null}}, {retweets: 1})
```

```
db.tweets.find({place: {$ne: null}, "place.country": {$nin: ["Argentina", "Brasil"]}, lang: "es"})
```

6. Mostrar los screen name de aquellos usuarios que tengan “Juan” como parte de su nombre.

```
db.tweets.find({"user.name":/Juan/}, {_id: 0, name: "$user.name", screen_name: "$user.screen_name"})
```

7. Mostrar de los 10 tweets con más retweets, su usuario y la cantidad de retweets.

```
db.tweets.find({},{_id: 0, user: "$user.id_str", retweet_count: 1}).sort({retweet_count: -1}).limit(10)
```

# Agregación

1. Mostrar de los 10 tweets con más retweets, su usuario y la cantidad de retweets. Ordenar la salida de forma ascendente.

```
db.tweets.aggregate(
[
  {$sort : {retweet_count : -1}},
  {$limit: 10},
  {$project: {_id: 0, user: "$user.id_str", retweet_count: 1}}
])
```

2. Encontrar los 10 hashtags más usados.

```
db.tweets.aggregate(
[
  {$unwind: "$entities.hashtags"},
  {$project: {hashtags: "$entities.hashtags.text"}}, 
	{$group: {
			_id: "$hashtags",
			count: {$count:{}} 
		}},
  {$sort: {count: -1}}
])
```

```
db.tweets.aggregate(
[
  {$unwind: "$entities.hashtags"},
  {$project: {hashtags: "$entities.hashtags.text"}}, 
	{$group: {
			_id: "$hashtags",
			count: {$sum:1} 
		}},
  {$sort: {count: -1}}
])
```