<script setup>
import { RouterLink, RouterView } from "vue-router";
import Header from "./components/Header.vue"
</script>
<template>
  <img id="left-corner" src="@/assets/images/left-corner.png">
  <img id="right-corner" src="@/assets/images/right-corner.png">
  <Header/>
  <RouterView />
</template>
<style lang="scss">
  #right-corner{
    position: absolute;
    z-index: -1;
    right: -0.2rem;
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

  @media screen and (max-width: 800px) {
    #right-corner{
      visibility: hidden;
    }
    #left-corner{
      visibility: hidden;
    }
  }
</style>

