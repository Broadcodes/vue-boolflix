<template>
  <header>
    <a href=""><img class="logo" src="../assets/img/boolflix_logo.png" alt="Boolflix"></a>
    <div class="navigationBar">
      <div class="navSx">
        <ul>
          <li>Home</li>
          <li>Serie</li>
          <li>Film</li>
          <li>Aggiunti di recente</li>
          <li>La mia lista</li>
        </ul>
      </div>
      <div class="navDx">
        <ul>
          <li><i class="fa-solid fa-magnifying-glass" @click="viewSearch"></i></li>
          <!-- <li><i class="fa-solid fa-filter" @click="filterSearch"></i></li> -->
          <li><i class="fa-solid fa-bell"></i></li>
          <li><img src="https://picsum.photos/200/300?random=0" alt="My Profile"></li>
        </ul>
        <div class="searchMoviesAndSeries">
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
      // viewAreaFilterSearchBox: false
    };
  },
  methods: {
    searchUserMovies() {
      this.$emit('searchMovies', this.searchMoviesText);
      this.searchMoviesText = '';
    },
    viewSearch() {
      const areaSearchBox = document.querySelector(".searchMoviesAndSeries");

      if (this.viewAreaSearchBox) {
        this.viewAreaSearchBox = false;
        areaSearchBox.classList.remove("view");
      } else {
        this.viewAreaSearchBox = true;
        areaSearchBox.classList.add("view");
      }
    },
    // filterSearch() {
    //   const areaSearchBox = document.querySelector(".searchMoviesAndSeries");

    //   if (this.viewAreaFilterSearchBox) {
    //     this.viewAreaFilterSearchBox = false;
    //     areaSearchBox.classList.remove("view");
    //   } else {
    //     this.viewAreaFilterSearchBox = true;
    //     areaSearchBox.classList.add("view");
    //   }
    // }
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
      right: 230px;
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
    color: #ccc;

    li {
      list-style-type: none;
      margin: 0 12px;
      cursor: pointer;

      .active,
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
  }
}
</style>