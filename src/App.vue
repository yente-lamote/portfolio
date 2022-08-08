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
    padding: 1rem;
    nav{
      width: 90%;
      margin:auto;
      display: flex;
      justify-content: space-between;
      a{
        font-size: 18px;
        padding: 1.5rem;
        display: block;
        color: $dark-blue-primary;
      }
      a:hover{
        color:$light-blue-primary;
      }
      ul{
        display: flex;
      }
    }
  }
</style>
