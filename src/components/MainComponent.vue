<template>
  <div>
    <div class="card" v-for="(item, index) in dataListObj" :key="item.id">

      <div v-if="index < (dataListObj.length / 2)">
        <p>Titolo: {{ item.title }}</p>
        <p>Titolo Originale: {{ item.original_title }}</p>
        <img :src="setFlagIcon(item.original_language)" :alt="item.title" @error="replaceFlagNotFound">
        <p>Voto: {{ item.vote_average }}</p>
      </div>
      <div v-else>
        <p>Titolo: {{ item.name }}</p>
        <p>Titolo Originale: {{ item.original_name }}</p>
        <img :src="setFlagIcon(item.original_language)" :alt="item.name" @error="replaceFlagNotFound">
        <p>Voto: {{ item.vote_average }}</p>
      </div>      
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
      switch (country) {
        case 'en':
          country = 'GB';
          break;
      }

        return "https://www.countryflagicons.com/FLAT/32/" + country.toUpperCase() + ".png";
    },
    replaceFlagNotFound(e){
        e.target.src = errorFlagIcon;
    }
  },
  props: {
    dataListObj: Array,
  },
};
</script>
  
  <style lang="scss" scoped>
    .card{
      border: 1px solid #000;
      padding: 20px 50px;
      width: 40%;
      margin: 50px;
      background-color: #eee;
    }
</style>