<template>
  <div>
    <div v-for="item in dataMoviesListObj" :key="item.id">
      <p>Titolo: {{ item.title }}</p>
      <p>Titolo Originale: {{ item.original_title }}</p>
      <p>Lingua: {{ item.original_language }}</p>
      <p>Voto: {{ item.vote_average }}</p>
      <p>------------------------------------------------------------------------</p>
    </div>
  </div>
</template>
  
  <script>
export default {
  data() {
    return {};
  },
  props: {
    dataMoviesListObj: Array,
  },
};
</script>
  
  <style lang="scss" scoped>
</style>