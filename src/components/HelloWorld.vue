<template>
  <div class="body">
    <header>
      <h1>
        Anime Movies <br />
        To Numb The Pain
      </h1>
    </header>

    <div>
      <img id="background" :src="`https://images8.alphacoders.com/749/749455.png`" alt="">
    </div>

    <label for="movie-picker">Select a Movie!:</label>
    <select v-model="moviePicker">
      <option value="378064">A Silent Voice</option>
      <option value="12477">Grave of Fireflies</option>
      <option value="530079">Ride Your Wave</option>
      <option value="372058">Your Name.</option>
      <option value="10494">Perfect Blue</option>
      <option value="198375">The Garden of Words</option>
      <option value="504253">I Want to Eat Your Pancreas</option>
      <option value="92321">Into the Forest of Firefly Light</option>
      <option value="4935">Howl's Moving astle</option>
      <option value="568160">Weathering With You</option>
    </select>
    <button @click="getInfo">GET</button>

    <div v-if="movieInfo" class="grid-container basic-info">
      <h2>{{ movieInfo.title }}</h2> 
      <img :src="`https://image.tmdb.org/t/p/w500${movieInfo.poster_path}`" alt="">
      <iframe :src="`https://www.youtube.com/embed/${movieInfo.videos.results.filter((trailer) => trailer.type === 'Trailer').at(0).key}`" frameborder="0"></iframe>
    </div>

    <div v-if="movieInfo" class="grid-container detail-info"> 
      <h3>{{ movieInfo.origin_country }}</h3> 
      <h3>{{ movieInfo.release_date }}</h3> 
      <h3>{{ movieInfo.original_title }}</h3> 
      <p>Original Language:{{ movieInfo.original_language }}</p> 
      <p>Runtime:{{ movieInfo.runtime }}</p> 
      <p>Status:{{ movieInfo.status }}</p> 
      <p>Rating:{{ movieInfo.vote_average }}</p> 
    </div>
  </div>
</template>

<style scoped>
* {
  padding: 0;
  margin: 0;
  background-image: url('https://wall.alphacoders.com/big.php?i=749455');
  background-size: cover;
  background-repeat: no-repeat;
}


header h1 {
  border-radius: 15px;
  background-color: #4d4c7d;
  text-shadow: 5px 5px #827397;
  filter: drop-shadow(-10px 10px 20px #827397);
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  padding: 50px;
  font-weight: bold;
  line-height: 1 rem;
  text-align: left;
  color: #d8b9c3;
  text-align: left;
  padding: 2rem;
  margin: 0;
  font-size: 2rem;
  letter-spacing: 1px;
}

label {
  color: #d8b9c3;
  margin-right: 10px;
  font-size: 2rem;
  font-weight: bold;
}

.movie-picker {
 
display: flex;
align-items: center;
justify-content: center;
margin-bottom: 20px;
padding: 8px;
font-size: 1rem;
border-radius: 5px;
}

button {
margin-left: auto;
padding: 8px 15px;
border: none;
border-radius: 5px;
background-color: #d8b9c3;
color: white;
font-size: 2rem;
cursor: pointer;
filter: drop-shadow(-10px 10px 20px #827397);
}
button:hover {
background-color: #dba4b5;
color: white;
filter: drop-shadow(-10px 10px 10px #827397);
}

.grid-container {
display: grid;
grid-gap: 20px;
margin: 20px;
background-color: rgba(252, 210, 235, 0.25);
}

.basic-info {
font-size: 30px;
text-align: center;
color: white;
padding: 20px;
border-radius: 5px;
box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
background-color: rgba(252, 210, 235, 0.25);
}

.img {
width: 40px;
margin-right: 20px;
margin-bottom: 10px;
border-radius: 5px;
}

#movie-trailer {
width: 50%;
height: 500px;
padding: 3rem;
border: none;
border-radius: 5px;
}

.basic-info {
color: white;
justify-content: center;
padding: 20px;
border-radius: 5px;
box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
background-color: rgba(252, 210, 235, 0.25);
}

.movie-details {
margin-top: 0;
font-size: 1.5rem;
}

#movie-picker {
border-radius: 15px;
border-color: rgba(0, 0, 0, 0);
padding: 1rem;
font-size: 1.5rem;
background-color: #4d4c7d;
color: #d8b9c3;
filter: drop-shadow(-10px 10px 20px #827397);
font-family: Verdana, Geneva, Tahoma, sans-serif;
}

option:hover {
filter: drop-shadow(-10px 10px 10px #827397);
background-color: black;
}
</style>

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
      console.log(movieInfo.status)
    };

    return { moviePicker, movieInfo, getInfo };
  },
};
</script>