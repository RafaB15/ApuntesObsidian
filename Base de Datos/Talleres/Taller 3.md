```SQL
-- a)
movies_2000 = σ (year = 2000) movies

-- b)
movies_2000 = σ (year = 2000) movies

directors_2000 = π director_id (movies_directors ⨝ (movies_directors.movie_id = movies.id) movies_2000)

directors ⨝ (directors.id = movies_directors.director_id) directors_2000

-- c)

woody_allen = π id(σ first_name = 'Woody' ∧ last_name='Allen' actors)

movies_allen = π movie_id (roles ⨝ (roles.actor_id = actors.id) woody_allen)

π name (movies_allen ⨝ (roles.movie_id = movies.id) movies)

-- d) 

hitler = π id(σ first_name = 'Adolf' ∧ last_name='Hitler' actors)

movies_hitler = π movie_id (roles ⨝ (roles.actor_id = actors.id) hitler)

π name (movies_hitler ⨝ (roles.movie_id = movies.id) movies)

-- e)

dir_gen = ρ genre ← movies_genres.genre π movies_directors.director_id, movies_genres.genre (movies_directors⨝(movies_directors.movie_id = movies_genres.movie_id) movies_genres)

genres = π genre movies_genres

dir_gen ÷ genres
```
Para hallar la película más nueva en cuestión de año lo que podemos hacer es un producto cartesiano entre dos tablas iguales con el nombre de la película y su año de estreno. Luego seleccionamos las filas en las que la fecha de salida de la primera fecha es menor a la segunda.
Todas las fechas que no son la mayor tendrán que aparecer en el resultado, pues si no son la mayor entonces en alguna fila hay otra fila que es mayor. Luego agarramos esta tabla y se la restamos a una con todas las fechas, lo cual nos tendría que dar como resultado una tabla con solo la película con mayor año.
![[Pasted image 20230908224340.png]]
![[Pasted image 20230908224324.png]]
*Primera y última fila no van*
![[Pasted image 20230908224350.png]]
![[Pasted image 20230908224353.png]]

Para ver actores que participaron en al menos 3 películas podemos hacer un triple producto cartesiano de nombre de actor y película para luego quedarnos con las filas en donde un mismo actor aparece con distintas películas.