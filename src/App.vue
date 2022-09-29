<!-- Milestone 3:
In questa milestone come prima cosa aggiungiamo la copertina del film o della serie
al nostro elenco. Ci viene passata dall’API solo la parte finale dell’URL, questo
perché poi potremo generare da quella porzione di URL tante dimensioni diverse.

Trasformiamo poi il voto da 1 a 10 decimale in un numero intero da 1 a 5, così da
permetterci di stampare a schermo un numero di stelle piene che vanno da 1 a 5,
lasciando le restanti vuote (troviamo le icone in FontAwesome).
Arrotondiamo sempre per eccesso all’unità successiva, non gestiamo icone mezze
piene -->

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
            `https://api.themoviedb.org/3/search/${typeSearch[index]}?api_key=${apiKey}&language=en-US&page=1&include_adult=false&query=${this.query}`
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
}
</style>
