<template>
  <div class="container">
    <div>
      <p>
        Notice: "This product uses the TMDb API but is not endorsed or certified
        by TMDb."
      </p>

      <section>
        Search by movie title: <input type="text" name="search" v-model="searchStr" /> <br />
        <br />
        <input type="button" value="Submit" v-on:click="searchMovies" />
      </section>

      <ul>
        <li v-for="movie in movies">
          Title: {{ movie.title }}<br />
          Popularity: {{ movie.popularity }}<br />
          Poster: <img src={movie.poster_path}><br />
        </li>
      </ul>

    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import axios from "axios";

let apiKey = "172a12cc6c8b8f90f9ef7274436b435e";

export default Vue.extend({
  computed: {
    movies(): array {
      return [];
    },
    searchStr(): string {
      return "";
    }
  },
  methods: {
    searchMovies(): function {
      axios
        .get(`https://api.themoviedb.org/3/search/movie?api_key=${apiKey}&language=en-US&query=${searchStr}&page=1&include_adult=false`)
        .then((json) => {
          console.log(json)
          this.movies = json.data.results
          });
    },
  }
});
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
