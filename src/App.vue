<template>
  <div id="app">
    <!-- All'avvio del sito mostra l'intro di boolflix -->
    <!-- La variabile playIntro è settata a true già all'avvio, per poi passare a false mediante
         un setTimeout -->
    <div v-if="playIntro === true" class="conteinerIntro">
      <video id="intro" autoplay muted>
        <source src="@/assets/img/Netflix_intro.mp4" type="video/mp4">
      </video>
    </div>
    <!-- Allo scattare del playIntro a false viene mostrata la pagina Home del sito -->
    <div v-else>
      <header>
        <!-- Nell'header vengono passati i dati acquisiti dall'API con il metodo getApiData -->
        <!-- La stessa barra header ritorna dei valori che serviranno per le altre pagine -->
        <HeaderComponent :listMoviesObj="dataSearchArr" @searchMovies="getSearchMovies"
          @ResearchInProgress="getResearch" @pageSelected="changePage" />
      </header>

      <!-- Qui sono presenti tutti i componenti che costituisco la pagina HomePage -->
      <main>
        <!-- La variabile pageMenu contiene un dato che proviene dall'header.
             Sta ad indicare quale pagina viene cliccato dall'utente nel menu di navigazione.
             In base alla scelta dell'utente viene quindi mostrata la pagina desiderata-->
        <div v-if="pageMenu === 'home'">
          <HomepageContainer />
        </div>
        <div v-else-if="pageMenu === 'series'">
          <SeriesHome />
        </div>
        <div v-else-if="pageMenu === 'movies'">
          <MoviesHome />
        </div>
        <div v-else-if="pageMenu === 'recentlyAdded'">
          <RecentlyAdded />
        </div>
        <div v-else-if="pageMenu === 'myList'">
          <MyList />
        </div>
        <div v-else-if="pageMenu === 'research'">
          <MainComponent :dataListObj="dataSearchArr" :currentPage="page" :maxPage="maxPage"
          @changePage="getNewPage" />
        </div>
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
import SeriesHome from "./components/seriesHome.vue";
import MoviesHome from "./components/moviesHome.vue";
import RecentlyAdded from "./components/recentlyAdded.vue";
import MyList from "./components/myList.vue";

export default {
  name: "App",
  data() {
    return {
      query: "",
      dataSearchArr: [],
      page: '1',
      maxPage: 0,
      playIntro: true,
      pageMenu: '',
    };
  },
  methods: {
    getApiData() {
      let typeSearch = ["movie", "tv"];
      let arr = [];

      for (let index = 0; index < typeSearch.length; index++) {
        // Genero una chiamata ad axios per ottenere i dati da un API.
        // L'url di seguito ha la query esterna in quanto verrà modificata dall'utente
        // in base alla ricerca dei film che vorrà eseguire
        axios
          .get(
            `https://api.themoviedb.org/3/search/${typeSearch[index]}?api_key=${apiKey}&language=it-IT&page=${this.page}&include_adult=false&query=${this.query}`
          )
          .then(({ data, status }) => {
            if (status === 200) {
              // Assegno i dati contenuti nell'array di oggetti contenuto nell'API
              // alla variabile globale di tipo Array
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
    },
    changePage(pageMenuSelect) {
      // Funzione per applicare al menu la classe active
      this.pageMenu = pageMenuSelect;
      let menu = ['home', 'series', 'movies', 'recentlyAdded', 'myList']

      for (let i = 0; i < menu.length; i++) {
        document.getElementById(`${menu[i]}`).classList.remove('active');
      }

      document.getElementById(`${this.pageMenu}`).classList.add('active');
    },
    getResearch(value) {
      this.pageMenu = value;
    }
  },
  components: {
    HeaderComponent,
    HomepageContainer,
    MainComponent,
    SeriesHome,
    MoviesHome,
    RecentlyAdded,
    MyList
  },
  mounted() {
    // Il setTimeout serve per modificare la variabile playIntro in
    // modo da interrompere la riproduzione della intro ad inizio schermata
    setTimeout(() => {
      this.playIntro = false;
    }, 4200);
    this.pageMenu = 'home';
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
  .bg-page {
    height: calc(100vh - 65px);
    overflow-y: auto;
    background: rgb(20, 20, 20);
    background: linear-gradient(180deg, rgba(20, 20, 20, 1) 0%, rgb(24, 24, 24) 100%);
    padding-bottom: 50px;
  }

  .conteinerIntro {
    height: 100vh;
    overflow: hidden;

    video {
      width: 100%;
      height: 100%;
      object-fit: cover;
      visibility: 100%;
      transition: visibility 1s;
    }

    .visibilityIn {
      visibility: 0%;
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
