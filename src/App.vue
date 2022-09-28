<template>
  <div id="app">
    <header>
      <HeaderComponent />
    </header>
    
    <main>
      <HomepageContainer />

    </main>
  </div>
</template>

<script>
  import HeaderComponent from './components/headerComponent.vue';
  import HomepageContainer from './components/homepageContainer.vue';


export default {
  name: 'App',
  components: {
    HeaderComponent,
    HomepageContainer,
}
}
</script>

<style lang="scss">
#app {
 
}
</style>
