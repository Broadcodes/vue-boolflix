<template>
  <div>
    <div class="containerCard">
      <CardMovies v-for="(cardMovie, index) in dataListObj" :key="index" :cardMoviesData="cardMovie" :indexMoviesData="index"/>
      <CardSeries v-for="(cardSerie, index) in dataListObj" :key="cardSerie.id" :cardSeriesData="cardSerie" :indexSeriesData="index"/>
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
    },
    components: { 
      CardMovies,
      CardSeries
    }
};
</script>
  
<style lang="scss" scoped>
.containerCard {
  display: flex;
  flex-wrap: wrap;
  height: calc(100vh - 65px);
  padding: 10px 30px;
  overflow-y: scroll;
  background: rgb(20, 20, 20);
  background: linear-gradient(180deg, rgba(20, 20, 20, 1) 0%, rgb(90, 90, 90) 100%);
}
</style>