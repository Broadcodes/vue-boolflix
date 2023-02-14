<template>
  <div class="bg-page">
    <!-- Slider con effetto specchio -->
    <CarouselHomePage />
    <!-- Seleziona lettera da alfabeto -->
    <SelectLetter @valueLetter="getValueLetter" />
    <!-- i più visti -->
    <h2>I più visti</h2>
    <TheMostViewed :dataQuery="dataArr" />
    <!-- i più votati -->
    <h2>I più votati</h2>
    <TheMostVoted :dataQuery="dataArr" />
    <!-- cos'è boolflix -->
    <h2>Cos'è Boolflix</h2>
    <MoreInfoBoolflix />
    <FooterComponent />
  </div>
</template>

<script>
import axios from "axios";
import { apiKey } from "@/env/apiKey";

import CarouselHomePage from './carouselHomePage.vue';
import TheMostViewed from './theMostViewed.vue';
import TheMostVoted from './theMostVoted.vue';
import SelectLetter from "./selectLetter.vue";
import MoreInfoBoolflix from "./moreInfoBoolflix.vue";
import FooterComponent from "./footerComponent.vue";


export default {
  name: 'homepageContainer',
  data() {
    return {
      query: "",
      dataArr: [],
    }
  },
  components: {
    CarouselHomePage,
    TheMostViewed,
    TheMostVoted,
    SelectLetter,
    MoreInfoBoolflix,
    FooterComponent
  },
  methods: {
    getApiDataHomepage(query) {
      let typeSearch = ["movie", "tv"];
      let arr = [];

      for (let index = 0; index < typeSearch.length; index++) {
        // Genero una chiamata ad axios per ottenere i dati da un API.
        // L'url di seguito ha la query esterna in quanto verrà modificata dall'utente in base alla ricerca dei film che vorrà eseguire
        axios
          .get(
            `https://api.themoviedb.org/3/search/${typeSearch[index]}?api_key=${apiKey}&language=it-IT&page=1&include_adult=false&query=${query}`
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
    getValueLetter(value) {
      this.query = value;
      this.dataArr = this.getApiDataHomepage(this.query);
    }
  },
  created() {
    this.dataArr = this.getApiDataHomepage("A");
  }
};
</script>

<style lang="scss" scoped>
h2 {
  color: #fff;
  padding: 30px;
  font-size: 1.3rem;
}

h2:nth-child(7) {
  margin: 60px 0;
  font-size: 2.5rem;
}
</style>