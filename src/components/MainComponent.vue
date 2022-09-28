<template>
  <div>
    <div v-for="item in dataMoviesListObj" :key="item.id">
      <p>Titolo: {{ item.title }}</p>
      <p>Titolo Originale: {{ item.original_title }}</p>
      <img :src="setFlagIcon(item.original_language)" :alt="item.original_language" @error="replaceFlagNotFound">
      <p>Voto: {{ item.vote_average }}</p>
      <p>------------------------------------------------------------------------</p>
    </div>
  </div>
</template>
  
  <script>
import errorFlagIcon from "@/assets/ErrorFlag/world.png";

export default {
  data() {
    return {
        
    };
  },
  methods:{
    setFlagIcon(country){
        return "https://www.countryflagicons.com/FLAT/32/" + country.toUpperCase() + ".png";
    },
    replaceFlagNotFound(e){
        e.target.src = errorFlagIcon;
    }
  },
  props: {
    dataMoviesListObj: Array,
  },
};
</script>
  
  <style lang="scss" scoped>
</style>