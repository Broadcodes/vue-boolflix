<template>
  <div>
    <div class="containerCards">
      <div v-for="(card, index) in getSort()" :key="index">
        <div class="card">
          <img :src="getPosterPath('w300', card.backdrop_path)" :alt="card.title" @error="changeImg">

          <div v-if="card.title !== '' || card.name !== '' ">
            <h2>{{card.title}}</h2>
            <h2>{{card.name}}</h2>
          </div>
          <div v-else>
            <h2>Dato non presente</h2>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'theMostViewed',
  data() {
    return {
      dataCards: [],
    }
  },
  props: {
    dataQuery: Array
  },
  methods: {
    getPosterPath(size, posterPath) {
      return `https://image.tmdb.org/t/p/${size}${posterPath}`;
    },
    getSort() {
      let arr = [];
      let arrSort = [];

      this.dataQuery.forEach(element => {
        arr.push(element.popularity);
      });

      arr.sort(function (a, b) {
        return b - a;
      });

      for (let i = 0; i < arr.length; i++) {
        for (let j = 0; j < this.dataQuery.length; j++) {
          if (arr[i] === this.dataQuery[j].popularity) {
            arrSort.push(this.dataQuery[j]);
          }
        }
      }
      return arrSort;
    },
    changeImg(e) {
      e.target.src = "https://www.srservicesge.it/images/immagine_non_disponibile.png";
    },
  }
}
</script>

<style lang="scss" scoped>
.containerCards {
  width: 100%;
  overflow-x: auto;
  display: flex;
  color: #fff;

  .card {
    margin: 0 20px;

    img {
      min-width: 300px;
      max-width: 300px;
      min-height: 169px;
      max-height: 169px;
    }

    h2 {
      font-size: 1.3rem;
      margin: 10px 0;
    }
  }
}

::-webkit-scrollbar {
  height: 0.5em !important;
}
</style>