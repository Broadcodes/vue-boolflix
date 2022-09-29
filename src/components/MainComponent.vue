<template>
  <div>
    <div class="containerCard">
      <div class="card" v-for="(item, index) in dataListObj" :key="item.id">
        <img :src="getPosterPath('w185', item.poster_path)" :alt="item.title" />
        <div v-if="index < dataListObj.length / 2">
          <p>Titolo Movie: {{ item.title }}</p>
          <p>Titolo Originale: {{ item.original_title }}</p>
        </div>
        <div v-else>
          <p>Titolo Serie: {{ item.name }}</p>
          <p>Titolo Originale: {{ item.original_name }}</p>
        </div>
        <img
          :src="setFlagIcon(item.original_language)"
          :alt="item.name"
          @error="replaceFlagNotFound"
        />
        <p>Voto: {{ item.vote_average }}</p>
      </div>
    </div>
  </div>
</template>
  
  <script>
import errorFlagIcon from "@/assets/ErrorFlag/world.png";

export default {
  data() {
    return {};
  },
  methods: {
    getPosterPath(size, posterPath) {
      return `https://image.tmdb.org/t/p/${size}${posterPath}`;
    },
    setFlagIcon(country) {
      switch (country) {
        case "en":
          country = "GB";
          break;
      }

      return (
        "https://www.countryflagicons.com/FLAT/32/" +
        country.toUpperCase() +
        ".png"
      );
    },
    replaceFlagNotFound(e) {
      e.target.src = errorFlagIcon;
    },
  },
  props: {
    dataListObj: Array,
  },
};
</script>
  
  <style lang="scss" scoped>
.containerCard{
  display: flex;
  flex-wrap: wrap;

  .card {
  border: 1px solid #000;
  padding: 40px 50px 20px;
  width: calc(100% /3 - 100px);
  text-align: center;
  margin: 50px;
  background-color: #eee;

  img:nth-child(1){
    padding-bottom: 20px;
  }

  p {
    text-align: left;
  }
}
}


</style>