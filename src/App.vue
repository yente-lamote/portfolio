<script setup>
import Header from "./components/Header.vue"
import HomeView from "./views/HomeView.vue";
import TopRightBars from "./components/svg's/TopRightBars.vue";
import DotsNav from './components/DotsNav.vue';
import AboutView from "./views/AboutView.vue";
import Projects from "./views/Projects.vue";
import router from "./router";
import Contact from "./views/Contact.vue";
import { createSimpleExpression } from "@vue/compiler-core";
import AboutViewNew from "./views/AboutViewNew.vue";
</script>
<template>
  <TopRightBars></TopRightBars>
  <DotsNav></DotsNav>
  <Header></Header>
  <main>
    <HomeView class="page" :style="{'transform':`translateY(-${translateY}px)`}"></HomeView>
    <Projects class="page" :style="{'transform':`translateY(-${translateY}px)`}"></Projects>
    <!-- <AboutView class="page" :style="{'transform':`translateY(-${translateY}px)`}"></AboutView> -->
    <AboutViewNew class="page" :style="{'transform':`translateY(-${translateY}px)`}"></AboutViewNew>
    <Contact class="page" :style="{'transform':`translateY(-${translateY}px)`}"></Contact>
  </main>
   <div id="loading">
    <div id="loading-container">
      <p>
        Yente<span>.</span>
      </p>
      <div class="loading-dots" data-title=".dot-elastic">
          <div class="stage">
            <div class="dot-elastic"></div>
          </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
    data(){
      return{
        lastScrollTop:0,
        vh:0,
        pagesArray:["home","projects","about","experience","skills","contact"],
        pages:[
          {
            name:"home",
            pageTranslate:0,
            enter:this.homeEnter,
            leave:this.homeLeave
          },
          {
            name:"projects",
            pageTranslate:1,
            enter:this.projectEnter,
            leave:this.projectLeave
          },
          {
            name:"about",
            pageTranslate:2,
            page:2,
            enter:this.aboutEnter,
            leave:()=>{}
          },
          {
            name:"experience",
            pageTranslate:2,
            enter:this.aboutEnter,
            leave:()=>{}
          },
          {
            name:"skills",
            pageTranslate:2,
            enter:this.aboutEnter,
            leave:()=>{}
          },
          {
            name:"contact",
            pageTranslate:3,
            enter:this.contactEnter,
            leave:()=>{}
          }
        ],
        //is gelinkt aan index van de bovenstaande array
        currentPage:0,
        scrolling:false,
        to:{},
        from:{},
        xDown: null,
        yDown: null,
      }
    },
    watch:{
      $route (to, from){
        this.scrolling=true
        this.to=to
        this.from=from
        if(this.from.name){
          let prevPage = this.pages.filter(function(el){return el.name == from.name})[0]
          prevPage.leave()
        }
        let page = this.pages.filter(function(el){return el.name == to.name})[0]
        page.enter()
        this.currentPage=this.pages.indexOf(page)
        if(this.currentPage!=0){
          const tl = gsap.timeline()
          tl.to('#scroll-indicator-container',{'display':'none', duration:0})
        }
      }
    },
    computed:{
      translateY(){
        return this.vh*100*this.pages[this.currentPage].pageTranslate
      }
    },
    methods:{
      async aboutEnter(){
        let aboutPages = ["about","experience","skills"]
        if(!aboutPages.includes(this.from.name)){
          const tl = gsap.timeline({defaults:{duration:0.4,ease: Power1.easeIn},onComplete:this.animationComplete})
          tl.delay(0.3)
          await new Promise(resolve => setTimeout(resolve, 0.1));
          tl.add("start")
          tl.fromTo('#profile-picture',{'transform':'scale(0.6) translateY(-40%)'},{'transform':'scale(1) translateY(0)',duration:0.7, ease: Sine.easeOut},"start")
          tl.fromTo("#about nav ul li",{"transform":"translateY(20px)","opacity":0},{"transform":"translateY(0)","opacity":1, delay:0.4},"start")
          tl.fromTo(".tab",{"transform":"translateY(20px)","opacity":0},{"transform":"translateY(0)","opacity":1,delay:0.5},"start")
        }else{
          this.animationComplete();
        }
        
      },
      homeEnter(){
        const tl = gsap.timeline({defaults:{duration:0.7,delay:0},onComplete:this.animationComplete})
        /*!this.from.name?
          tl.delay(0.6)://wanneer pagina voor eerste keer ingeladen wordt
          tl.delay(0.6)*/
        tl.delay(0.6)
        tl.add("start")
        tl.fromTo('#scroll-indicator-container',{'transform':'translateY(100vh) translateX(-50%)','display':'none','opacity':0},{'display':'flex','transform':'translateY(0) translateX(-50%)','opacity':1},'start')
        tl.fromTo('#home-title',{'transform':'translate(-140%, 0)'},{'transform':'translate(0, 0)'},"start")
        //tl.fromTo('#face-wrapper',{'transform':'translate(140%, 0)'},{'transform':'translate(0, 0)'},"start")
        tl.fromTo('#face-wrapper',{'transform':'scale(0.4) translateY(-60%)'},{'transform':'scale(1) translateY(0)',ease: Sine.easeOut},'start')

        !this.from.name&&
        tl.fromTo('#top-right-bars',{'transform':'translate(100%, -100%)'},{'transform':'translate(0, 0)', duration:0.9},"start")
      },
      homeLeave(){
        const tl = gsap.timeline({defaults:{duration:0.6}})
        tl.to('#scroll-indicator-container',{'transform':'translateY(100vh)','display':'none','opacity':0})
      },
      /*aboutEnter(){
        const tl = gsap.timeline({defaults:{duration:0.7,ease: Power1.easeIn},onComplete:this.animationComplete})
        !this.from.name?
          tl.delay(0.55)://wanneer pagina voor eerste keer ingeladen wordt
          tl.delay(0.4)
        tl.add("start")
        tl.fromTo('#about-info',{'transform':'translate(-100%, 0)','opacity':'0'},{'transform':'translate(0, 0)','opacity':'1'},"start")
        tl.fromTo('.tagcloud',{'transform':'translate(140%, 0)','opacity':'0'},{'transform':'translate(0, 0)','opacity':'1'},"start")
      },*/
      contactEnter(){
        const tl = gsap.timeline({defaults:{duration:0.7,ease: Power1.easeIn},onComplete:this.animationComplete})
        !this.from.name?
          tl.delay(0.55)://wanneer pagina voor eerste keer ingeladen wordt
          tl.delay(0.35)
        tl.fromTo('#contact-form',{'transform':'translate(200%, 0)'},{'transform':'translate(0, 0)'},"loadFirst")
        tl.fromTo('#left-contact-side-container',{'transform':'translate(-200%, 0)'},{'transform':'translate(0, 0)'},"loadFirst")
      },
      projectEnter(){
        const tlOne = gsap.timeline({defaults:{duration:0.7},onComplete:this.animationComplete})
        tlOne.delay(0.3)
        tlOne.add("start")
        tlOne.fromTo('#mockups-desktop, #projects-mobile img',{'transform':'scale(0.4) translateY(-60%)'},{'transform':'scale(1) translateY(0)',ease: Sine.easeOut},"start")
        tlOne.fromTo('#projects-mobile h1',{'transform':'translateX(-140%)'},{'transform':'translateX(0)'},"start")
        tlOne.add("butons")
        tlOne.fromTo('#projects-mobile .button-full',{'opacity':'0', 'transform':'translateY(10px)'},{'opacity':'1', 'transform':'translateY(0)',duration:0.5},"butons")
        tlOne.fromTo('#projects-mobile .button-border',{'opacity':'0', 'transform':'translateY(10px)'},{'opacity':'1', 'transform':'translateY(0)',duration:0.6,delay:0.1},"butons")
        
        const tlTwo = gsap.timeline({defaults:{duration:0.4}})
        tlTwo.delay(0.5)
        tlTwo.add("start")
        tlTwo.fromTo('#projects-desktop h1',{'opacity':'0'},{'opacity':'1'},"start")
        tlTwo.fromTo('#projects-desktop h2',{'opacity':'0', 'transform':'translateY(20px)'},{'opacity':'1', 'transform':'translateY(0)',delay:0.3},"start")
        tlTwo.fromTo('#lead-project-main-info',{'opacity':'0', 'transform':'translateY(20px)'},{'opacity':'1', 'transform':'translateY(0)', delay:0.5},"start")
        tlTwo.fromTo('#lead-project-api-info',{'opacity':'0', 'transform':'translateY(20px)'},{'opacity':'1', 'transform':'translateY(0)', delay:0.6},"start")
        tlTwo.fromTo('#projects-desktop #icons',{'opacity':'0', 'transform':'translateY(20px)'},{'opacity':'1', 'transform':'translateY(0)', delay:0.7},"start")
        tlTwo.fromTo('#projects-desktop .button-full',{'opacity':'0', 'transform':'translateY(35px)'},{'opacity':'1', 'transform':'translateY(0)',duration:0.5,delay:0.6},"start")
        tlTwo.fromTo('#projects-desktop .button-border',{'opacity':'0', 'transform':'translateY(35px)'},{'opacity':'1', 'transform':'translateY(0)',duration:0.6,delay:0.7},"start")
        
        //tl.fromTo('#lid',{'transform':'perspective(3000px) rotateX(-80deg)'},{'transform':'perspective(3000px) rotateX(0deg)',duration: 0.6,ease: 'none',})
      },
      projectLeave(){
        const tl = gsap.timeline({defaults:{duration:0.6}})
        //tl.to('#lid',{'transform':'perspective(3000px) rotateX(-90deg)'})
      },
      async animationComplete(){
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
      },
      getTouches(event) {
        return event.touches ||             // browser API
        event.originalEvent.touches; // jQuery
      },   
      handleTouchStart(event){
        const firstTouch = this.getTouches(event)[0];                                      
        this.xDown = firstTouch.clientX;                                      
        this.yDown = firstTouch.clientY;     
      },
      handleTouchMove(event){
        if ( ! this.xDown || ! this.yDown ) {
            return;
        }

        var xUp = event.touches[0].clientX;                                    
        var yUp = event.touches[0].clientY;

        var xDiff = this.xDown - xUp;
        var yDiff = this.yDown - yUp;
                                                                            
        if ( Math.abs( xDiff ) > Math.abs( yDiff ) ) {/*most significant*/
            if ( xDiff > 0 ) {
                /* right swipe */ 
            } else {
                /* left swipe */
            }                       
        } else {
            if ( yDiff > 0 ) {
              this.handleScrollDown()
            } else { 
              this.handleScrollUp()
            }                 
            router.push({name:this.pages[this.currentPage].name})                                                
        }
        /* reset values */
        this.xDown = null;
        this.yDown = null;      
      }

    },
    mounted(){
      this.calculateVh();
      window.addEventListener("resize",this.calculateVh)
      window.addEventListener("wheel", this.checkScrollDirection);
      document.addEventListener('touchstart', this.handleTouchStart, false);        
      document.addEventListener('touchmove', this.handleTouchMove, false);
      
      //https://stackoverflow.com/questions/2264072/detect-a-finger-swipe-through-javascript-on-the-iphone-and-android
      const tl = gsap.timeline({defaults:{duration:0.7}})
      tl.delay(0.5)
      
      tl.fromTo('#loading',{'transform':'translateY(0)'},{'transform':'translateY(-100%)'})
      tl.to('#loading',{'display':'none', duration:0})
    }
}
</script>
<style lang="scss">
  #loading-container{
    position: absolute;
    left: 50%;
    transform: translate(-50%, -50%);
    top:50%;
  }
  .dot-elastic {
  position: relative;
  width: 7px;
  height: 7px;
  border-radius: 50%;
  background-color: $pink;
  color: $pink;
  animation: dotElastic 1s infinite linear;
  left: 50%;
}

.dot-elastic::before, .dot-elastic::after {
  content: '';
  display: inline-block;
  position: absolute;
  top: 0;
}

.dot-elastic::before {
  left: -12px;
  width: 7px;
  height: 7px;
  border-radius: 50%;
  background-color: $pink;
  color: $pink;
  animation: dotElasticBefore 1s infinite linear;
}

.dot-elastic::after {
  left: 12px;
  width: 7px;
  height: 7px;
  border-radius: 50%;
  background-color: $pink;
  color: $pink;
  animation: dotElasticAfter 1s infinite linear;
}

@keyframes dotElasticBefore {
  0% {
    transform: scale(1, 1);
  }
  25% {
    transform: scale(1, 1.5);
  }
  50% {
    transform: scale(1, 0.67);
  }
  75% {
    transform: scale(1, 1);
  }
  100% {
    transform: scale(1, 1);
  }
}

@keyframes dotElastic {
  0% {
    transform: scale(1, 1);
  }
  25% {
    transform: scale(1, 1);
  }
  50% {
    transform: scale(1, 1.5);
  }
  75% {
    transform: scale(1, 1);
  }
  100% {
    transform: scale(1, 1);
  }
}

@keyframes dotElasticAfter {
  0% {
    transform: scale(1, 1);
  }
  25% {
    transform: scale(1, 1);
  }
  50% {
    transform: scale(1, 0.67);
  }
  75% {
    transform: scale(1, 1.5);
  }
  100% {
    transform: scale(1, 1);
  }
}
  main{
    width: 100vw;
    position:relative;
    overflow: hidden;
    overflow-x: hidden;
  }
  .page{
    height: 100vh; /* Fallback for browsers that do not support Custom Properties */
    height: calc(var(--vh, 1vh) * 100);
    width:80vw;
    margin:auto;
    overflow:hidden;
    position: relative;
    // -webkit-transition: all 0.5s linear;
    // -moz-transition: all 0.5s linear;
    // -o-transition: all 0.5s linear;
    // transition: all 0.5s linear;
    transition: all 1000ms cubic-bezier(0.645, 0.045, 0.355, 1) 0s;
    transition-property: all;
    transition-duration: 1000ms;
    transition-timing-function: cubic-bezier(0.645, 0.045, 0.355, 1);
    transition-delay: 0s;
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
      font-size: 2em;
      font-size: 2.4rem;
      color: $white;
      font-weight: bold;
      padding:0.4rem 0;
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
    .page{
      width: 90%;
    }
  }
  @media screen and (max-width: 800px) {
    .page{
      width: 100%;
    }
  }
  
</style>

