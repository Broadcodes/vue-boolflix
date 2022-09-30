<template>
  <div>
    <div class="bg-mainCard">
      <div class="containerCard">
        <CardMovies v-for="(cardMovie, index) in dataListObj" :key="index" :cardMoviesData="cardMovie"
          :indexMoviesData="index" />
        <CardSeries v-for="(cardSerie, index) in dataListObj" :key="cardSerie.id" :cardSeriesData="cardSerie"
          :indexSeriesData="index" />
      </div>
      <div class="page">
        <i v-if="(parseInt(currentPage) - 1) != 0" class="fa-solid fa-angle-left" @click="prevPage"></i>
        <i v-else></i>
        <div class="numberPage">
          <p v-if="(parseInt(currentPage) - 1) != 0">{{parseInt(currentPage) - 1}}</p>
          <p v-else></p>
          <p>{{currentPage}}</p>
          <p v-if="currentPage < maxPage">{{parseInt(currentPage) + 1}}</p>
          <p v-else></p>
        </div>
        <i v-if="currentPage < maxPage" class="fa-solid fa-angle-right" @click="nextPage"></i>
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
    }
  }
};
</script>
  
<style lang="scss" scoped>
.bg-mainCard {
  height: calc(100vh - 65px);
  overflow-y: scroll;
  background: rgb(20, 20, 20);
  background: linear-gradient(180deg, rgba(20, 20, 20, 1) 0%, rgb(90, 90, 90) 100%);

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