<!-- Milestone 2:
Trasformiamo la stringa statica della lingua in una vera e propria bandiera della
nazione corrispondente, gestendo il caso in cui non abbiamo la bandiera della
nazione ritornata dall’API (le flag non ci sono in FontAwesome).
Allarghiamo poi la ricerca anche alle serie tv. Con la stessa azione di ricerca
dovremo prendere sia i film che corrispondono alla query, sia le serie tv, stando
attenti ad avere alla fine dei valori simili (le serie e i film hanno campi nel JSON di
risposta diversi, simili ma non sempre identici) -->

<template>
  <div id="app">
    <header>
      <HeaderComponent
        :listMoviesObj="dataMoviesArr"
        @searchMovies="getSearchMovies"
      />
    </header>

    <main>
      <HomepageContainer/>
      <MainComponent :dataMoviesListObj="dataMoviesArr" />
    </main>
  </div>
</template>

<script>
import axios from "axios";

import HeaderComponent from "./components/headerComponent.vue";
import HomepageContainer from "./components/homepageContainer.vue";
import MainComponent from "./components/MainComponent.vue";

export default {
  name: "App",
  data() {
    return {
      query: "",
      dataMoviesArr: [],
    };
  },
  methods: {
    getApiMovies() {
      let arr = [];
      // Genero una chiamata ad axios per ottenere i dati da un API.
      // L'url di seguito ha la query esterna in quanto verrà modificata dall'utente in base alla ricerca dei film che vorrà eseguire
      axios
        .get(
          "https://api.themoviedb.org/3/search/movie?api_key=5e425de4522465f0801227e0eeeb6782&language=en-US&page=1&include_adult=false&query=" +
            this.query
        )
        .then(({ data, status }) => {
          if (status === 200) {
            // Assegno i dati contenuti nell'array di oggetti contenuto nell'API alla variabile globale di tipo Array
            arr.push(...data.results);
          }
        })
        .catch((e) => {
          e.message;
        });

      return arr;
    },
    getSearchMovies(textSearch) {
      // Ottengo dall'input presente in headerComponent il valore che viene digitato dall'utente
      // Il dato che mi arriva viene inserito nella query in modo da ottenere la ricerca dei film
      this.query = textSearch;
      // Tutti i dati presenti nell'API vengono salvati nell'array dataMoviesArr
      this.dataMoviesArr = this.getApiMovies();
    },
  },
  components: {
    HeaderComponent,
    HomepageContainer,
    MainComponent
}
};
</script>

<style lang="scss">
#app {
}
</style>
