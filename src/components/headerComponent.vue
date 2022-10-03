<template>
  <header>
    <img @click="getValuePage('home')" class="logo" src="../assets/img/boolflix_logo.png" alt="Boolflix">
    <div class="navigationBar">
      <div class="navSx">
        <!-- Barra di navigazione sinistra -->
        <ul>
          <li id="home" class="active" @click="getValuePage('home')">Home</li>
          <li id="series" @click="getValuePage('series')">Serie</li>
          <li id="movies" @click="getValuePage('movies')">Film</li>
          <li id="recentlyAdded" @click="getValuePage('recentlyAdded')">Aggiunti di recente</li>
          <li id="myList" @click="getValuePage('myList')">La mia lista</li>
        </ul>
      </div>
      <div class="navDx">
        <!-- Barra di navigazione destra -->
        <ul>
          <li><i class="fa-solid fa-magnifying-glass" @click="viewSearch"></i></li>
          <li><i class="fa-solid fa-bell"></i></li>
          <li><img src="https://picsum.photos/200/300?random=0" alt="My Profile"></li>
        </ul>
        <div class="searchMoviesAndSeries" @mouseleave="viewSearch">
          <input type="text" v-model="searchMoviesText" @keyup.enter="searchUserMovies" />
          <button @click="searchUserMovies">Cerca</button>
        </div>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  name: 'headerComponent',
  data() {
    return {
      searchMoviesText: '',
      viewAreaSearchBox: false,
    };
  },
  methods: {
    // restituisce il valore inserito dall'utente per effettuare la ricerca
    searchUserMovies() {
      this.$emit('searchMovies', this.searchMoviesText);
      this.searchMoviesText = '';
      this.$emit('ResearchInProgress', 'research');
    },
    viewSearch() {
      // Mostra o nasconde l'input per la ricerca dei movies o delle series
      const areaSearchBox = document.querySelector(".searchMoviesAndSeries");

      if (this.viewAreaSearchBox) {
        this.viewAreaSearchBox = false;
        areaSearchBox.classList.remove("view");
      } else {
        this.viewAreaSearchBox = true;
        areaSearchBox.classList.add("view");
      }
    },
    getValuePage(value) {
      // Restituiesce il valore della pagina cliccata dall'utente nella barra di navigazione
      this.$emit('pageSelected', value);
    }
  },
  props: {
    listMoviesArr: Array
  }
};
</script>

<style lang="scss" scoped>
@import url('https://fonts.googleapis.com/css2?family=Red+Hat+Display:wght@500&display=swap');

header {
  background-color: #141414;
  width: 100%;
  height: 65px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 50px;

  .logo {
    width: 100px;
    cursor: pointer;
  }

  .navigationBar {
    flex-grow: 1;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding-left: 40px;
    font-family: 'Red Hat Display', sans-serif;
  }

  .navDx {
    position: relative;

    .searchMoviesAndSeries {
      width: 0px;
      position: absolute;
      display: flex;
      align-items: center;
      top: 50%;
      transform: translateY(-15px);
      right: 180px;
      overflow: hidden;
      transition: width 1s;

      input {
        width: 270px;
        height: 30px;
      }

      button {
        margin-left: 15px;
        padding: 5px 15px;
        background-color: #252525;
        color: #fff;
        border: 3px solid #3a3a3a;
        border-radius: 5px;
        cursor: pointer;

        &:hover {
          background-color: #373737;
        }
      }
    }
  }

  .searchMoviesAndSeries.view {
    width: 350px;
  }

  .navSx ul,
  .navDx ul {
    display: flex;
    align-items: center;
    color: rgb(168, 168, 168);

    li {
      list-style-type: none;
      margin: 0 12px;
      cursor: pointer;

      &:hover {
        color: #fff;
      }

      i {
        font-size: 1.3rem;
        padding: 0 3px;
      }

      img {
        width: 40px;
        height: 40px;
        border-radius: 50px;
        cursor: default;
      }
    }

    .active {
      color: #fff;
    }
  }
}

@media screen and (max-width: 860px) {
  .navSx ul li {
    font-size: 1.3vw;
  }
}
</style>