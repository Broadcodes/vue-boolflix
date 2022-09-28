<template>
  <header>
    <input type="text" v-model="searchMoviesText" @keyup.enter="searchUserMovies"/>
    <button @click="searchUserMovies">Cerca</button>
  </header>
</template>

<script>
export default {
  data() {
    return {
        searchMoviesText: '',
    };
  },
  methods:{
    searchUserMovies(){
        this.$emit('searchMovies', this.searchMoviesText);
    }
  },
  props:{
    listMoviesArr: Array
  }
};
</script>

<style lang="scss" scoped>
</style>