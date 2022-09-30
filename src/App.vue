<!-- Milestone 4:
Trasformiamo quello che abbiamo fatto fino ad ora in una vera e propria webapp,
creando un layout completo simil-Netflix:
● Un header che contiene logo e search bar
● Dopo aver ricercato qualcosa nella searchbar, i risultati appaiono sotto forma
di “card” in cui lo sfondo è rappresentato dall’immagine di copertina (consiglio
la poster_path con w342)
● Andando con il mouse sopra una card (on hover), appaiono le informazioni
aggiuntive già prese nei punti precedenti più la overview -->

<template>
  <div id="app">
    <header>
      <HeaderComponent
        :listMoviesObj="dataSearchArr"
        @searchMovies="getSearchMovies"
      />
    </header>

    <main>
      <HomepageContainer v-if="dataSearchArr.length === 0" />
      <MainComponent v-else :dataListObj="dataSearchArr" />
    </main>
  </div>
</template>

<script>
import axios from "axios";
import { apiKey } from "@/env/apiKey";

import HeaderComponent from "./components/headerComponent.vue";
import HomepageContainer from "./components/homepageContainer.vue";
import MainComponent from "./components/MainComponent.vue";

export default {
  name: "App",
  data() {
    return {
      query: "",
      dataSearchArr: [],
    };
  },
  methods: {
    getApiData() {
      let typeSearch = ["movie", "tv"];
      let arr = [];

      for (let index = 0; index < typeSearch.length; index++) {
        // Genero una chiamata ad axios per ottenere i dati da un API.
        // L'url di seguito ha la query esterna in quanto verrà modificata dall'utente in base alla ricerca dei film che vorrà eseguire
        axios
          .get(
            `https://api.themoviedb.org/3/search/${typeSearch[index]}?api_key=${apiKey}&language=it-IT&page=1&include_adult=false&query=${this.query}`
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
      }
      return arr;
    },
    getSearchMovies(textSearch) {
      // Ottengo dall'input presente in headerComponent il valore che viene digitato dall'utente
      // Il dato che mi arriva viene inserito nella query in modo da ottenere la ricerca dei film
      this.query = textSearch;
      this.dataSearchArr = this.getApiData();
    },
  },
  components: {
    HeaderComponent,
    HomepageContainer,
    MainComponent,
  },
};
</script>

<style lang="scss">
  * {
    box-sizing: border-box;
    margin: 0px;
    padding: 0px;
  }
  
  body {
    font-family: sans-serif;
  }

#app {
  ::-webkit-scrollbar {
  width: 0.8em;
  height: 0.8em;
  background: #686868;
  margin-right: 10px;
}

::-webkit-scrollbar-thumb {
  min-height: 0.8em;
  min-width: 0.8em;
  -webkit-border-radius: 10px;
  background-color: #cfcfcf;
  border: none;
}

::-webkit-scrollbar-thumb:active {
  background-color: #adadad;
  border: none;
}
}
</style>
