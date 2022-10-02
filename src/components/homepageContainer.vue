<template>
  <div class="bg-page">
    <!-- Slider con effetto specchio -->
    <CarouselHomePage/>
    <!-- i più visti -->
    <h2>I più visti</h2>
    <TheMostViewed />
    <!-- i più votati -->
    <h2>I più votati</h2>
    <TheMostVoted />
    <h2>Movies</h2>
    <!-- Movie -->
    <MoviesHome />
    <h2>Series</h2>
    <!-- Serie -->
    <SeriesHome />
  </div>
</template>

<script>
import CarouselHomePage from './carouselHomePage.vue';
import TheMostViewed from './theMostViewed.vue';
import TheMostVoted from './theMostVoted.vue';
import MoviesHome from './moviesHome.vue';
import SeriesHome from './seriesHome.vue';


export default {
  components: {
    CarouselHomePage,
    TheMostViewed,
    TheMostVoted,
    MoviesHome,
    SeriesHome
  }
};
</script>

<style lang="scss" scoped>
h2 {
  color: #fff;
  padding: 20px;
  font-size: 1.3rem;
}
</style>