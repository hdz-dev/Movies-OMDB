<script>
  // @ts-nocheck
  import { onMount } from "svelte";

  onMount(() => {
    api();
  });

  let hero = "";
  let movie;
  let stars = [1, 2, 3, 4, 5];
  async function api(values) {
    await fetch(
      "https://www.omdbapi.com/?apikey=29bdd042&t=" + values + "&plot=full"
    )
      .then((response) => response.json())
      .then((data) => {
        console.log(data);
        movie = data;
        console.log(movie);
        // Aquí puedes realizar operaciones adicionales con los datos recibidos
      })
      .catch((error) => console.error(error));
  }


</script>

<div class="flex flex-col justify-center">
  <div class=" flex flex-row m-auto bg-white w-1/2 rounded-3xl px-4">
    <input class="outline-none w-full"   
    type="text" 
    placeholder="Buscar..." 
    bind:value={hero} />

    <img
      on:click={() => api(hero)}
      class="w-auto h-4 m-auto"
      src="../busqueda.png"
      alt=""
    />
  </div>

  <div>
    {#if movie}
      <div
        class="flex flex-row bg-whitex w-auto rounded-xl pt-2 px-4 mx-4 mt-4"
      >
        <div class="w-1/2">
          <img class="rounded-xl" src={movie.Poster} alt="" />
          <p class="text-md text-center text-white my-2 font-bold">
            {movie.Title}
          </p>
        </div>

        <div id="info" class="w-1/2 px-4">
          <p class="text-xs text-white">Director</p>
          <p class="text-xs text-white font-bold mb-2">{movie.Director}</p>
          <p class="text-xs text-white">Genero</p>
          <p class="text-xs text-white font-bold mb-2">{movie.Genre}</p>
          <p class="text-xs text-white">Año</p>
          <p class="text-xs text-white font-bold mb-2">{movie.Year}</p>
          <p class="text-xs text-white">Duración</p>
          <p class="text-xs text-white font-bold mb-2">{movie.Runtime}</p>
          <p class="text-xs text-white">Clasificación</p>
          <p class="text-xs text-white font-bold mb-2">{movie.Rated}</p>
        </div>
      </div>

      <div id="stars" class="px-8 flex flex-row">
        <p class="text-md text-white font-boldx  my-auto mr-2">Calificación IMDB</p>
        
        {#each stars as star, index}
          <ul class="my-1 flex list-none gap-1 p-0" data-te-rating-init>
            <li>
              <span
                class="text-primary [&>svg]:h-5 [&>svg]:w-5"
                title="Bad"
                data-te-rating-icon-ref
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  fill={(index < Math.round(movie.imdbRating / 2))  ? 'full' : 'none'}
                  viewBox="0 0 24 24"
                  stroke-width="1.5"
                  stroke="white"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    d="M11.48 3.499a.562.562 0 011.04 0l2.125 5.111a.563.563 0 00.475.345l5.518.442c.499.04.701.663.321.988l-4.204 3.602a.563.563 0 00-.182.557l1.285 5.385a.562.562 0 01-.84.61l-4.725-2.885a.563.563 0 00-.586 0L6.982 20.54a.562.562 0 01-.84-.61l1.285-5.386a.562.562 0 00-.182-.557l-4.204-3.602a.563.563 0 01.321-.988l5.518-.442a.563.563 0 00.475-.345L11.48 3.5z"
                  />
                </svg>
              </span>
            </li>
          </ul>
        {/each}
        <p class="text-xs text-white font-bold ml-2 my-auto">({movie.imdbRating})</p>
      </div>

      <div class="flex flex-row justify-center my-4">
        <button class="bg-blackx margin-auto rounded-3xl border-2 border-white text-white px-4 py-1">Mas detalles</button>
      </div>
      
      <div />

      <div class="w-auto px-8 mt-2">
        <p class="text-xs text-white">{movie.Plot}</p>
      </div>
    {:else}
      <div>
        <p />
      </div>
    {/if}
  </div>
</div>
