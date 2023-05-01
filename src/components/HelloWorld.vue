<template>
  <div class="body">
    <header>
      <h1>
        Anime Movies <br />
        To Numb The Pain
      </h1>
    </header>

    <label for="moviePicker">Select a Movie!:</label>
    <select v-model="moviePicker">
      <option value="378064">A Silent Voice</option>
      <option value="12477">Grave of Fireflies</option>
      <option value="530079">Ride Your Wave</option>
      <option value="372058">Your Name.</option>
      <option value="10494">Perfect Blue</option>
      <option value="198375">The Garden of Words</option>
      <option value="504253">I Want to Eat Your Pancreas</option>
      <option value="92321">Into the Forest of Firefly Light</option>
      <option value="4935">Howl's Moving Castle</option>
      <option value="568160">Weathering With You</option>
    </select>
    <button @click="getInfo">GET</button>

    <div v-if="movieInfo" class="info-container">
      
      <img :src= "`https://image.tmdb.org/t/p/w500${movieInfo.poster_path}`" alt="">
      <div class="info">
        <h1>{{ movieInfo.title }}</h1> 
        <p>Release Date: {{movieInfo.release_date}} | Popularity: {{movieInfo.popularity}} | Runtime: {{movieInfo.runtime}} | Genre: {{movieInfo.genres.map((genre) => { return genre.name} )}}</p>
        <p>Vote Average: {{movieInfo.vote_average}} | Vote Count: {{movieInfo.vote_count}}</p>
        <h2>Overview:</h2>
        <p> {{ movieInfo.overview }}</p>
        <iframe :src= "`https://www.youtube.com/embed/${movieInfo.videos.results.filter((trailer) => trailer.type === 'Trailer').at(0).key}`" frameborder="0"></iframe>
        <p>"{{movieInfo.tagline}}"</p>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import axios from "axios";
import { TMDB_API_KEY } from "./key.js";

export default {
  name: "MovieInfo",
  setup() {
    const moviePicker = ref("378064");
    const movieInfo = ref(null);

    const getInfo = async () => {
      const response = await axios.get(
        `https://api.themoviedb.org/3/movie/${moviePicker.value}`,
        {
          params: {
            api_key: TMDB_API_KEY,
            append_to_response: "videos",
          },
        }
      );
      movieInfo.value = response.data;
      console.log(movieInfo.value);
    };

    return { moviePicker, movieInfo, getInfo };
  },
};
</script>

<style scoped>
.body {
  margin: 20px;
  background-color: aqua;
  font-family: Verdana, Geneva, Tahoma, sans-serif;
}
</style>
