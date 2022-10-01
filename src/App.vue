<template>
  <div id="app">
    <div v-if="playIntro === true" class="conteinerIntro">
      <video id="intro" autoplay muted>
        <source src="@/assets/img/Netflix_intro.mp4" type="video/mp4">
      </video>
    </div>
    <div v-else>
      <header>
        <HeaderComponent :listMoviesObj="dataSearchArr" @searchMovies="getSearchMovies" />
      </header>

      <main>
        <HomepageContainer v-if="dataSearchArr.length === 0" />
        <MainComponent v-else :dataListObj="dataSearchArr" :currentPage="page" :maxPage="maxPage"
          @changePage="getNewPage" />
      </main>
    </div>
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
      page: '1',
      maxPage: 0,
      playIntro: true
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
            `https://api.themoviedb.org/3/search/${typeSearch[index]}?api_key=${apiKey}&language=it-IT&page=${this.page}&include_adult=false&query=${this.query}`
          )
          .then(({ data, status }) => {
            if (status === 200) {
              // Assegno i dati contenuti nell'array di oggetti contenuto nell'API alla variabile globale di tipo Array
              arr.push(...data.results);
              this.maxPage += parseInt(data.total_pages);
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
    getNewPage(page) {
      this.page = page;
      this.getSearchMovies(this.query);
    }
  },
  components: {
    HeaderComponent,
    HomepageContainer,
    MainComponent,
  },
  mounted() {
    setInterval(() => {
      document.getElementById('intro').classList.add('opacityIn');
    }, 4000);

    setInterval(() => {
      this.playIntro = false;
    }, 4200);
  }
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
  .conteinerIntro {
    height: 100vh;
    overflow: hidden;

    video {
      width: 100%;
      object-fit: cover;
      opacity: 100%;
      transition: opacity 1s;
    }

    .opacityIn {
      opacity: 0%;
    }

  }

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
