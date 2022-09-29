<template>
  <div>
    <div class="containerCard">
      <div class="card" v-for="(item, index) in dataListObj" :key="item.id">
        <img :src="getPosterPath('w342', item.poster_path)" :alt="item.title" />
        <div v-if="index < dataListObj.length / 2">
          <div v-if="item.title === item.original_title">
            <p>Titolo Movie: {{ item.title }}</p>
          </div>
          <div v-else>
            <p>Titolo Movie: {{ item.title }}</p>
            <p>Titolo Originale: {{ item.original_title }}</p>
          </div>
        </div>
        <div v-else>
          <div v-if="item.title === item.original_title">
            <p>Titolo Movie: {{ item.title }}</p>
          </div>
          <div v-else>
            <p>Titolo Series: {{ item.title }}</p>
            <p>Titolo Originale: {{ item.original_title }}</p>
          </div>
        </div>
        <img :src="setFlagIcon(item.original_language)" :alt="item.original_language" @error="replaceFlagNotFound" />
        <div>
          <p>Vote:
            <span v-if="toFiveStars(item.vote_average) === 1">
              <i class="starYellow fa-solid fa-star"></i>
              <i class="starGray fa-regular fa-star"></i>
              <i class="starGray fa-regular fa-star"></i>
              <i class="starGray fa-regular fa-star"></i>
              <i class="starGray fa-regular fa-star"></i>
            </span>
            <span v-else-if="toFiveStars(item.vote_average) === 2">
              <i class="starYellow fa-solid fa-star"></i>
              <i class="starYellow fa-solid fa-star"></i>
              <i class="starGray fa-regular fa-star"></i>
              <i class="starGray fa-regular fa-star"></i>
              <i class="starGray fa-regular fa-star"></i>
            </span>
            <span v-else-if="toFiveStars(item.vote_average) === 3">
              <i class="starYellow fa-solid fa-star"></i>
              <i class="starYellow fa-solid fa-star"></i>
              <i class="starYellow fa-solid fa-star"></i>
              <i class="starGray fa-regular fa-star"></i>
              <i class="starGray fa-regular fa-star"></i>
            </span>
            <span v-else-if="toFiveStars(item.vote_average) === 4">
              <i class="starYellow fa-solid fa-star"></i>
              <i class="starYellow fa-solid fa-star"></i>
              <i class="starYellow fa-solid fa-star"></i>
              <i class="starYellow fa-solid fa-star"></i>
              <i class="starGray fa-regular fa-star"></i>
            </span>
            <span v-else-if="toFiveStars(item.vote_average) === 5">
              <i class="starYellow fa-solid fa-star"></i>
              <i class="starYellow fa-solid fa-star"></i>
              <i class="starYellow fa-solid fa-star"></i>
              <i class="starYellow fa-solid fa-star"></i>
              <i class="starYellow fa-solid fa-star"></i>
            </span>
          </p>

        </div>


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
    viewOneTitle(translatedTitle, originalTitle){

      if(translatedTitle === originalTitle){
        return `Titolo: ${translatedTitle}`;
      } else {
        return `Titolo: ${translatedTitle}
        Titolo Originale: ${originalTitle}`;
      }

    },
    toFiveStars(vote) {
      return Math.ceil(vote / 2);
    },
    getPosterPath(size, posterPath) {
      return `https://image.tmdb.org/t/p/${size}${posterPath}`;
    },
    setFlagIcon(country) {
      switch (country) {
        case "en":
          country = "GB";
          break;
        case "ja":
          country = "jp";
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
.containerCard {
  display: flex;
  flex-wrap: wrap;

  .card {
    border: 1px solid #000;
    padding: 40px 20px;
    width: calc(100% /3 - 100px);
    text-align: center;
    margin: 50px;
    background-color: #eee;

    img:nth-child(1) {
      padding-bottom: 20px;
    }

    p {
      text-align: left;
    }

    .starYellow {
      color: rgb(238, 202, 42);
    }

    .starGray {
      color: rgb(199, 199, 199);
    }
  }
}
</style>