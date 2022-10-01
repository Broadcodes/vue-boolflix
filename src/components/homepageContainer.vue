<template>
  <div class="bg-page">
    <!-- Slider con effetto specchio -->
    <CarouselHomePage />
    <!-- i più visti -->
    <TheMostViewed />
    <!-- i più votati -->
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
.homepage {
  // background-color: #141414;
}
</style>