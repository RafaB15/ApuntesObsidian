**a. Muestre las películas dirigidas por ' Hitchcock' de la década de 1950 (del año 1950 al año 1959):**

h_id = π id (σ last_name = 'Hitchcock' directors)

h_movies = π movies_directors.movie_id (movies_directors ⨝ (movies_directors.director_id = directors.id) h_id)

π movies.name (movies ⨝ (movies.id = movies_directors.movie_id ∧ movies.year ≥ 1950 ∧ movies.year ≤ 1959) h_movies)

![[Pasted image 20230909020610.png]]

**b. Muestre la/las películas que fueron dirigidas juntos por los hermanos Coen (Ethan y Joel). Tenga en cuenta que pueden existir otros Coen en la base**

coen_id = π id σ (last_name = 'Coen' ∧ (first_name = 'Ethan' ∨ first_name = 'Joel')) directors 

coen_m = π directors.id, movies_directors.movie_id (movies_directors ⨝ (movies_directors.director_id = directors.id) coen_id)

coen_brothers_movies = π movies_directors.movie_id (σ (coen_m_copy.id ≠ directors.id ∧ coen_m_copy.movie_id = movies_directors.movie_id
) (ρ coen_m_copy (coen_m) ⨯ coen_m))

π name (coen_brothers_movies ⨝ (movies_directors.movie_id = movies.id) movies)

![[Pasted image 20230909020645.png]]

**c. Nombre todas las películas en que participó por lo menos un actor de la película 'Memento'.**

m_id = π id (σ (name = 'Memento') movies)

m_actors = ρ m_actors (π roles.actor_id (roles ⨝ (roles.movie_id = movies.id) m_id))

m_actors_movies = π roles.movie_id (m_actors ⨝ (roles.actor_id = m_actors.actor_id) roles)

π movies.name (movies ⨝ (roles.movie_id = movies.id) m_actors_movies)

![[Pasted image 20230909020716.png]]

**d. Mostrar los nombres y años de filmación, de la/las películas animadas (Animation) más vieja/s de la base.**

animation_id = π movies_genres.movie_id (σ genre = 'Animation' movies_genres)

ani_1 = π movies.year, movies.id, movies.name (movies ⨝ (movies.id = movies_genres.movie_id) animation_id)

ani_vs_ani = ani_1 ⨯ ρ ani_2 (ani_1)

not_oldest = π movies.year, movies.name (σ (movies.year	> ani_2.year) (ani_vs_ani))

π movies.year, movies.name ani_vs_ani - not_oldest

![[Pasted image 20230909020742.png]]

**e. Muestre la/las películas que han sido dirigidas con más de 2 directores**

two_plus_directed_movies = π movies_directors.movie_id (σ (movies_directors.movie_id = md_copy_1.movie_id ∧ movies_directors.movie_id = md_copy_2.movie_id ∧ md_copy_1.movie_id = md_copy_2.movie_id ∧ movies_directors.director_id ≠ md_copy_1.director_id ∧ movies_directors.director_id ≠ md_copy_2.director_id ∧ md_copy_1.director_id ≠ md_copy_2.director_id) (movies_directors x ρ md_copy_1 (movies_directors) ⨯ ρ md_copy_2 (movies_directors)))

π movies.name (two_plus_directed_movies ⨝ (movies_directors.movie_id = movies.id) movies)

![[Pasted image 20230909020809.png]]