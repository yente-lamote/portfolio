

<template>
  <div id="home-container">
    <section id="info">
      <p class="greeting">Hi, my name is</p>
      <h1>Yente Lamote</h1>
      <h2 id="subtitle">I'm a simple guy who's passionate about<br>solving problems with code.</h2>
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
    components: { Face },
    mounted() {
      document.addEventListener('mousemove', this.onMouseMove)
      window.addEventListener('resize', this.updateViewportSize)
      const tl = gsap.timeline({defaults:{duration:0.4}})
      tl.fromTo('#info',{'transform':'translateY(40px)',opacity:0.5},{'transform':'translateY(0px)',opacity:1,duration:0.4, ease:Power2.easeOut})
      tl.add("subtitle-face")
      tl.fromTo('#subtitle',{'transform':'translateY(5px)',opacity:0},{'transform':'translateY(0px)',opacity:1},"subtitle-face")
      tl.fromTo('#face',{scale:0.95, opacity:0, 'transform':'translateY(20px)'},{scale:1.01, opacity:1,'transform':'translateY(0px)', duration:0.4},"subtitle-face")
      tl.add('face-binary')
      tl.to('#face',{scale:1, duration:0.2},'face-binary')
      tl.fromTo('#binary',{scaleX:0.5, opacity:0},{scale:1.03, opacity:0.3,ease:Power2.easeIn},'face-binary')
      tl.add("border-buttons-binary")
      tl.to('#binary',{scale:1,opacity:0.3,duration:1,ease:Power2.easeOut},"border-buttons-binary")
      tl.fromTo('#info',{"border-left":"2px solid #F5F9FF"},{"border-left":"2px solid #1D53FF"},"border-buttons-binary")
      tl.fromTo('#about-me-button, #contact-me-button',{opacity:0},{opacity:1},"border-buttons-binary")
    },
}
</script>
<style lang="scss">

  
  #home-container{
    width:86%;
    padding: 3em 0;
    margin: 1em auto;
    display: flex;
    vertical-align: center;
    justify-content: center;
    align-items:flex-start;
    align-content:flex-start;
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
      line-height: 1.3em;
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