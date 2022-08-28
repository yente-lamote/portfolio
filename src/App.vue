<script setup>
import Header from "./components/Header.vue"
import HomeView from "./views/HomeView.vue";
import TopRightBars from "./components/svg's/TopRightBars.vue";
import DotsNav from './components/DotsNav.vue';
import AboutView from "./views/AboutView.vue";
import Projects from "./views/Projects.vue";
import router from "./router";
</script>
<template>
  <TopRightBars></TopRightBars>
  <DotsNav></DotsNav>
  <Header></Header>
  <main>
    <HomeView class="page" :style="{'transform':`translateY(-${translateY}px)`}"></HomeView>
    <AboutView class="page" :style="{'transform':`translateY(-${translateY}px)`}"></AboutView>
    <Projects class="page" :style="{'transform':`translateY(-${translateY}px)`}"></Projects>
  </main>
   <div id="loading">
      <p>
        Yente<span>.</span>
      </p>
  </div>
</template>
<script>
export default {
    data(){
      return{
        lastScrollTop:0,
        vh:0,
        pages:["home","about","projects","contact"],
        currentPage:0,
        scrolling:false,
      }

    },
    watch:{
      $route (to, from){
        this.scrolling=true
        this.scrolling=false
      }
    }, 
    computed:{
      translateY(){
        
        return this.vh*100*this.currentPage
      }
    },
    methods:{
      checkScrollDirection(event){
        if(!this.scrolling){
          this.scrolling=true
          this.checkScrollDirectionIsUp(event)?
            this.handleScrollUp():
            this.handleScrollDown()
            router.push({name:this.pages[this.currentPage]})
          this.scrolling=false
        }
      },
      handleScrollUp(){
        if(this.currentPage>0){
          this.currentPage-=1
        }
        
      },
      handleScrollDown(){
        if(this.currentPage<this.pages.length-1){
          this.currentPage+=1
        }
      },

      checkScrollDirectionIsUp(event) {
        if (event.wheelDelta) {
          return event.wheelDelta > 0;
        }
        return event.deltaY < 0;
      },

      calculateVh(){
          this.vh = window.innerHeight * 0.01;
          // Then we set the value in the --vh custom property to the root of the document
          document.documentElement.style.setProperty('--vh', `${this.vh}px`);
      }
    },
    mounted(){
      window.addEventListener("resize",this.calculateVh)
      this.calculateVh();
      window.addEventListener("wheel", this.checkScrollDirection);
      const tl = gsap.timeline({defaults:{duration:0.7}})
      tl.delay(0.3)
      tl.fromTo('#loading',{'top':'0%'},{'top':'-100%'})
      tl.to('#loading',{'display':'none', duration:0})
    }
}
</script>
<style lang="scss">
  main{
    width: 80vw;
    margin:auto;
    position:relative;
    overflow: hidden;
    overflow-x: hidden;
  }
  .page{
    height: 100vh; /* Fallback for browsers that do not support Custom Properties */
    height: calc(var(--vh, 1vh) * 100);
    position: relative;
    overflow: hidden;
  }
  #app{
    height: 100vh; /* Fallback for browsers that do not support Custom Properties */
    height: calc(var(--vh, 1vh) * 100);
    overflow: hidden;
    overflow-x: hidden;

  }
  body{
    height: 100vh; /* Fallback for browsers that do not support Custom Properties */
    height: calc(var(--vh, 1vh) * 100);
    overflow:hidden;
    background: linear-gradient(#002D40 60%, #001720);
    background-attachment: fixed;
    overflow-x: hidden;

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

  #loading{
    background-color:#001720;
    width:100vw;
    height: 100vh;
    z-index: 2;
    top: 0;
    left: 0;
    position: absolute;
    p{
      overflow: hidden;
      position: absolute;
      top:50%;
      left:50%;
      font-size: 2em;
      transform: translateX(-50%) translateY(-50%);
      font-size: 2.4rem;
      color: $white;
      font-weight: bold;
      padding:0.75rem 0;
      margin-right:1.5rem;
      span{
        color: $pink;
        border-radius: 25%;
      }
      svg{
        display: block;
      }
    }
  }
  @media screen and (max-width: 1650px) {
    main{
      width: 90%;
    }
  }
  @media screen and (max-width: 800px) {
    main{
      width: 100%;
    }
  }
  
</style>

