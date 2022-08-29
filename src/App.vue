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
        pagesArray:["home","about","projects","contact"],
        pages:[
          {
            name:"home",
            position:0,
            start:this.homeStart,
            end:this.homeEnd
          },
          {
            name:"about",
            position:1,
            start:this.aboutStart,
            end:()=>{}
          },
          {
            name:"projects",
            position:2,
            start:()=>{this.scrolling=false},
            end:()=>{}
          },
          {
            name:"contact",
            position:3,
            start:()=>{this.scrolling=false},
            end:()=>{}
          }
        ],
        currentPage:0,
        scrolling:false,
        to:{},
        from:{}
      }
    },
    watch:{
      $route (to, from){
        this.scrolling=true
        this.to=to
        this.from=from
        if(this.from.name){
          let prevPage = this.pages.filter(function(el){return el.name == from.name})[0]
          prevPage.end()
        }
        let page = this.pages.filter(function(el){return el.name == to.name})[0]
        page.start()
        this.currentPage=page.position
      }
    },
    computed:{
      translateY(){
        return this.vh*100*this.currentPage
      }
    },
    methods:{
      homeStart(){
        const tl = gsap.timeline({defaults:{duration:0.9},onComplete:this.animationComplete})
        !this.from.name?
          tl.delay(0.4)://wanneer pagina voor eerste keer ingeladen wordt
          tl.delay(0.5)
        tl.add("loadFirst")
        tl.to('#scroll-indicator-container',{'display':'flex','bottom':'5vh'},'loadFirst')
        tl.fromTo('#home-title',{'margin-left':'-100%',opacity:0},{'margin-left':'0px',opacity:1, ease:Power2.easeOut,},"loadFirst")
        tl.fromTo('#face-wrapper',{'right':'-100%',opacity:0},{'right':'0',opacity:1, ease:Power2.easeOut},"loadFirst")
        !this.from.name&&
        tl.fromTo('#top-right-bars',{'margin-top':'-100%',"margin-right":"-100%"},{'margin-top':'0',"margin-right":"0", ease:Power2.easeOut, duration:1.3},"home")
      },
      homeEnd(){
        const tl = gsap.timeline({defaults:{duration:0.5},onComplete:this.animationComplete})
        tl.to('#scroll-indicator-container',{'bottom':'-100vh','display':'none'})
      },
      aboutStart(){
        const tl = gsap.timeline({defaults:{duration:0.9},onComplete:this.animationComplete})
        tl.delay(0.7)
        tl.add("loadFirst")
        tl.fromTo('#about-info',{'left':'-35%',opacity:0},{'left':'0',opacity:1, ease:Power2.easeOut,},"loadFirst")
        tl.fromTo('.tagcloud',{'right':'-100%',opacity:0},{'right':'3%',opacity:1, ease:Power2.easeOut},"loadFirst")
      },
      animationComplete(){
        console.log("complete")
        this.scrolling=false;
      },
      checkScrollDirection(event){
        if(!this.scrolling){
          this.scrolling=true
          this.checkScrollDirectionIsUp(event)?
            this.handleScrollUp():
            this.handleScrollDown()
            router.push({name:this.pages[this.currentPage].name})
        }
      },
      handleScrollUp(){
        if(this.currentPage>0){
          this.currentPage-=1
        }else{
          this.scrolling=false
        }
      },
      handleScrollDown(){
        if(this.currentPage<Object.keys(this.pages).length-1){
          this.currentPage+=1
        }else{
          this.scrolling=false
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
      this.calculateVh();
      window.addEventListener("resize",this.calculateVh)
      window.addEventListener("wheel", this.checkScrollDirection);
      //document.addEventListener('touchstart', handleTouchStart, false);        
      //document.addEventListener('touchmove', handleTouchMove, false);
      //https://stackoverflow.com/questions/2264072/detect-a-finger-swipe-through-javascript-on-the-iphone-and-android
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
    -webkit-transition: all 0.7s linear;
    -moz-transition: all 0.7s linear;
    -o-transition: all 0.7s linear;
    transition: all 0.7s linear;
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

