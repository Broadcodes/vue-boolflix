<template>
  <div>
    <div class="bg-page">
      <!-- Pagina in cui vengono mostrate tutte le card ricercate dall'utente  -->
      <div class="containerCard">
        <CardMovies v-for="cardMovie in getMovies()" :key="cardMovie.id" :cardMoviesData="cardMovie" />
        <CardSeries v-for="cardSerie in getSeries()" :key="cardSerie.id" :cardSeriesData="cardSerie" />
      </div>
      <!-- è possibile scorrere la ricerca andando da una pagina all'altra -->
      <div class="page">
        <i v-if="(parseInt(currentPage) - 1) != 0" class="fa-solid fa-angle-left" @click="prevPage"></i>
        <i v-else></i>
        <div class="numberPage">
          <p v-if="(parseInt(currentPage) - 1) != 0">{{parseInt(currentPage) - 1}}</p>
          <p v-else></p>


          <p>{{currentPage}}</p>

          
          <p v-if="getNumberPage() === 40">{{parseInt(currentPage) + 1}}</p>
          <p v-else></p>
        </div>
        <i v-if="getNumberPage() === 40" class="fa-solid fa-angle-right" @click="nextPage"></i>
        <i v-else></i>
      </div>
    </div>
  </div>
</template>
  
<script>
import CardMovies from "@/components/cardMovies";
import CardSeries from "@/components/cardSeries";

export default {
  name: 'MainComponent',
  data() {
    return {};
  },
  props: {
    dataListObj: Array,
    currentPage: String,
    maxPage: Number
  },
  components: {
    CardMovies,
    CardSeries
  },
  methods: {
    prevPage() {
      this.$emit('changePage', (parseInt(this.currentPage) - 1).toString());
    },
    nextPage() {
      this.$emit('changePage', (parseInt(this.currentPage) + 1).toString());
    },
    getMovies() {
      let arrMovies = [];

      this.dataListObj.forEach(element => {
        if (element.title != '' && element.title != undefined) {
          arrMovies.push(element);
        }
      });

      return arrMovies;
    },
    getSeries(){
      let arrSeries = [];

      this.dataListObj.forEach(element => {
        if (element.name != '' && element.name != undefined) {
          arrSeries.push(element);
        }
      });

      return arrSeries;
    },
    getNumberPage(){

      let count = 0;
      
      for (let i = 0; i < this.dataListObj.length; i++) {
        count++
      }

      return count;
    }
  }
};
</script>
  
<style lang="scss" scoped>
.bg-page {
  .containerCard {
    display: flex;
    flex-wrap: wrap;
    padding: 10px 30px 50px;
  }

  .page {
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
    top: -30px;
    color: #fff;
    font-size: 1.5rem;

    i {
      margin: 0 100px;
      cursor: pointer;
    }

    .numberPage {
      display: flex;
      justify-content: space-between;
      align-items: center;
      width: 150px;

      p:nth-of-type(odd) {
        font-size: 1.2rem;
      }

      p:nth-of-type(even) {
        font-size: 2.5rem;
      }
    }
  }
}
</style>