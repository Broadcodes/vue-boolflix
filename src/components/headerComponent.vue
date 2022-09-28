<!-- Milestone 1:
Creare un layout base con una searchbar (un input e un button) in cui possiamo
scrivere completamente o parzialmente il nome di un film. Possiamo, cliccando il
bottone, cercare sull’API tutti i film che contengono ciò che ha scritto l’utente.
Vogliamo dopo la risposta dell’API visualizzare a schermo i seguenti valori per ogni
film trovato:
1. Titolo
2. Titolo Originale
3. Lingua
4. Voto -->

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