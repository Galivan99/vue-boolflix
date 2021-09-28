<template>
  <div id="app">
    
    <Header @performSearch="search" />

    <Main :movieCards="movies" />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Main from "./components/Main.vue";
import axios from "axios";
export default {
  name: "App",
  components: {
    Header,
    Main,
  },
  data() {
    return {
      apiUrl: "https://api.themoviedb.org/3/search/",
      apiKey: "77044b3f5f3cf322ff14c15889b611bc",
      movies: [],
    };
  },
  methods: {
    getMovies(apiParams) {
      axios.get(this.apiUrl + "movie", apiParams).then((response) => {
        console.log(this.apiUrl + "movie", apiParams);
        this.movies = response.data.results;
      });
    },
    search(searchText) {
      const paramsObj = {
        params: {
          api_key: this.apiKey,
          query: searchText,
        },
      };
      this.getMovies(paramsObj);
    },

  },
};
</script>

<style lang="scss">
@import "~bootstrap/scss/bootstrap";
@import "./style/generals";
body {
  background-color: grey;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: white;
}
</style>