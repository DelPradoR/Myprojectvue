<template>
    <Suspense>
      <div>
        <h2 v-if="selectedMovie">{{ selectedMovie }}</h2> <!-- Mostrar el nombre de la película seleccionada -->
        <table id="peliculas-table" class="table table-striped table-bordered" style="width: 80%">
          <thead>
            <tr>
              <th scope="col">Título</th>
              <th scope="col">Calificación</th>
              <th scope="col">IMDB</th>
            </tr>
          </thead>
          <tbody>
            <!-- Las filas se agregarán aquí dinámicamente -->
          </tbody>
        </table>
      </div>
    </Suspense>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const selectedMovie = ref(''); // Estado para almacenar el nombre de la película seleccionada

async function obtenerPeliculas() {
    let response = await fetch('https://dummyapi.online/api/movies');
    let peliculas = await response.json();

    let peliculasFiltradas = peliculas.map(pelicula => {
        return {
            movie: pelicula.movie,
            rating: pelicula.rating,
            imdb_url: pelicula.imdb_url
        };
    });

    agregarFilasTabla(peliculasFiltradas);
}

function agregarFilasTabla(peliculas) {
    const tbody = document.querySelector('#peliculas-table tbody');
    tbody.innerHTML = ''; // Limpiar el tbody antes de agregar nuevas filas

    peliculas.forEach(pelicula => {
        const fila = document.createElement('tr');

        const celdaMovie = document.createElement('td');
        celdaMovie.textContent = pelicula.movie;
        celdaMovie.className = 'col-titulo';
        celdaMovie.onclick = () => {
            selectedMovie.value = pelicula.movie; // Actualizar el estado con el nombre de la película
        };

        const celdaRating = document.createElement('td');
        celdaRating.textContent = pelicula.rating;
        celdaRating.className = 'col-rating';

        const celdaImdb_url = document.createElement('td');
        celdaImdb_url.textContent = pelicula.imdb_url;
        celdaImdb_url.className = 'col-imdb';

        fila.appendChild(celdaMovie);
        fila.appendChild(celdaRating);
        fila.appendChild(celdaImdb_url);

        tbody.appendChild(fila);
    });
}

onMounted(() => {
    obtenerPeliculas();
});
</script>

<style scoped>
#peliculas-table {
    margin: auto;
    border-collapse: collapse;
}

#peliculas-table th,
#peliculas-table td {
    padding: 12px;
    text-align: left;
    border: 1px solid rgb(42, 155, 248);
}

#peliculas-table th {
    background-color: rgb(42, 155, 248);
    font-weight: bold;
}

/* Estilo para las filas de la tabla */
#peliculas-table tr {
    background-color: black; /* Color de fondo negro para las filas */
}

/* Alternar color de fondo para filas impares */
#peliculas-table tr:nth-child(odd) {
    background-color: black; /* Color negro para filas impares */
}

/* Cambiar el color de fondo al pasar el mouse */
#peliculas-table tr:hover {
    background-color: rgb(42, 155, 248); /* Color al pasar el mouse */
}

.col-titulo {
    width: 40%;
    font-size: 1.2rem;
    cursor: pointer; /* Cambiar el cursor al pasar sobre el título */
}

.col-rating {
    color: green;
}

.col-imdb {
    width: 40%;
    font-size: 1rem;
}
</style>