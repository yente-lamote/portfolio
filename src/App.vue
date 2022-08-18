<script setup>
import { RouterLink, RouterView } from "vue-router";
import Header from "./components/Header.vue"
import HomeView from "./views/HomeView.vue";
</script>
<template>
  <img id="left-corner" src="@/assets/images/left-corner.png">
  <img id="right-corner" src="@/assets/images/right-corner.png">
  <img id="background" src="@/assets/images/background.png">
  <Header></Header>
  <main>
    <HomeView></HomeView>
  </main>
</template>
<style lang="scss">
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
    margin:auto
  }
  @media screen and (max-width: 800px) {
    #right-corner{
      visibility: hidden;
    }
    #left-corner{
      visibility: hidden;
    }
    main{
      width: 100%;
    }
  }
  
</style>

