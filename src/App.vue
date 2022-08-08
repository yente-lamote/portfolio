<script setup>
import { RouterLink, RouterView } from "vue-router";
import HelloWorld from "./components/HelloWorld.vue";
</script>

<template>
  <header>
    <nav>
        <RouterLink class="home" to="/">Home</RouterLink>
        <ul>
          <li>
            <RouterLink to="/about">About</RouterLink>
          </li>
          <li>
            <RouterLink to="/experience">Experience</RouterLink>
          </li>
          <li>
            <RouterLink to="/projects">Projects</RouterLink>
          </li>
          <li>
            <RouterLink to="/contact">Contact</RouterLink>
          </li>
          <li>
            <RouterLink to="/resume">Resume</RouterLink>
          </li>
        </ul>
    </nav>
  </header>
  <RouterView />
</template>

<style lang="scss">
  header{
    nav{
      width: 80%;
      margin:auto;
      display: flex;
      justify-content: space-between;
      .home{
        padding: 1rem;
      }
      a{
        padding: 1rem;
        display: block;
      }
      ul{
        display: flex;
      }
    }
  }
</style>
