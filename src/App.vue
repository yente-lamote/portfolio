<script setup>
import Header from "./components/Header.vue"
import HomeView from "./views/HomeView.vue";
import TopRightBars from "./components/svg's/TopRightBars.vue";
import DotsNav from './components/DotsNav.vue';
</script>
<template>
  <TopRightBars></TopRightBars>
  <DotsNav></DotsNav>
  <Header></Header>
  <main>
    <HomeView></HomeView>
  </main>
   
</template>
<style lang="scss">
  #app{
    height: 100%;
  }
  body{
    background: linear-gradient(#002D40 60%, #001720);
    height: 100vh;
  }
  #right-corner{
    position: absolute;
    z-index: -1;
    right:0;
    width:15rem;
    margin-top:-0.2rem;
  }
  #left-corner{
    position: absolute;
    z-index: -1;
    width:19rem;
    margin-left: -0.5rem;
    margin-top:-0.1rem;
  }
  #background{
    z-index: -2;
    position: absolute;
    width: 100vw;
    height: 88vh;
  }
  main{
    width: 80vw;
    margin:auto;
    height: 100vh;
    position:relative;
  }
  @media screen and (max-width: 800px) {
    main{
      width: 100%;
    }
  }
  
</style>

