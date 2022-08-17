

<template>
  <div id="home-container">
    <section id="info">
      <p class="greeting">Hi, my name is</p>
      <h1>Yente Lamote</h1>
      <h2>Software developer</h2>
      <a id="about-me-button" href="#">about me</a>
      <a id="contact-me-button" href="#">contact me</a>
    </section>
    <aside>
      <Face></Face>
      
    </aside>
  </div>
</template>

<script>
import Face from '../components/Face.vue';
export default{
    components: { Face }
}
</script>
<style lang="scss">

  
  #home-container{
    width:86%;
    margin: 3em auto;
    display: flex;
    vertical-align: center;
    justify-content: center;
    align-items:flex-start;
    align-content:flex-start;
    overflow:hidden
  }
  #info{
    margin-top: auto;
    margin-bottom: auto;
    position: relative;
    display: inline-block;
    border-left: 2px solid;
    padding: 0.5em 1em;
    border-color: $blue;
    overflow-block: hidden;
    .greeting{
      color:$grey;
      font-size: 2em;
    }
    h1{
      color: $dark-blue;
      font-size: 5rem;
      padding: 0.1rem 0;
    }
    h2{
      margin-top:0.5em;
      font-size: 1.3em;
      color: $grey;
      font-weight: normal;
    }
    #about-me-button{
      margin-top:2em;
      display: inline-block;
      border: 2px solid;
      border-color: $blue;
      border-radius: 10px;
      padding: 0.7em 1.5em;
      color:$blue;
    }
    #contact-me-button{
      padding:0.4em 1em;
      color: $grey;
    }
  }
  aside{
    width: 40%;
    margin-left: auto;
    display:inline-block;
    width: auto;
    position: relative;
  }
</style>