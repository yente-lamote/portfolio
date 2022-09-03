<script setup>
import Header from "./components/Header.vue"
import HomeView from "./views/HomeView.vue";
import TopRightBars from "./components/svg's/TopRightBars.vue";
import DotsNav from './components/DotsNav.vue';
import AboutView from "./views/AboutView.vue";
import Projects from "./views/Projects.vue";
import router from "./router";
import Contact from "./views/Contact.vue";
</script>
<template>
  <TopRightBars></TopRightBars>
  <DotsNav></DotsNav>
  <Header></Header>
  <main>
    <HomeView class="page" :style="{'transform':`translateY(-${translateY}px)`}"></HomeView>
    <AboutView class="page" :style="{'transform':`translateY(-${translateY}px)`}"></AboutView>
    <Projects class="page" :style="{'transform':`translateY(-${translateY}px)`}"></Projects>
    <Contact class="page" :style="{'transform':`translateY(-${translateY}px)`}"></Contact>
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
            start:this.contactStart,
            end:()=>{}
          }
        ],
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
        const tl = gsap.timeline({defaults:{duration:1,delay:0},onComplete:this.animationComplete})
        !this.from.name?
          tl.delay(0.6)://wanneer pagina voor eerste keer ingeladen wordt
          tl.delay(0.35)
        tl.add("loadFirst")
        tl.fromTo('#scroll-indicator-container',{'transform':'translateY(100vh)','display':'none','opacity':0},{'display':'flex','transform':'translateY(0)','opacity':1},'loadFirst')
        tl.fromTo('#home-title',{'transform':'translate(-140%, 0)'},{'transform':'translate(0, 0)'},"loadFirst")
        tl.fromTo('#face-wrapper',{'transform':'translate(140%, 0)'},{'transform':'translate(0, 0)'},"loadFirst")
        !this.from.name&&
        tl.fromTo('#top-right-bars',{'transform':'translate(100%, -100%)'},{'transform':'translate(0, 0)', duration:1.2},"loadFirst")
      },
      homeEnd(){
        const tl = gsap.timeline({defaults:{duration:0.6},onComplete:this.animationComplete})
        tl.to('#scroll-indicator-container',{'transform':'translateY(100vh)','display':'none','opacity':0})
      },
      aboutStart(){
        const tl = gsap.timeline({defaults:{duration:1},onComplete:this.animationComplete})
        !this.from.name?
          tl.delay(0.6)://wanneer pagina voor eerste keer ingeladen wordt
          tl.delay(0.35)
        tl.add("loadFirst")
        tl.fromTo('#about-info',{'transform':'translate(-100%, 0)','opacity':'0'},{'transform':'translate(0, 0)','opacity':'1'},"loadFirst")
        tl.fromTo('.tagcloud',{'transform':'translate(140%, 0)','opacity':'0'},{'transform':'translate(0, 0)','opacity':'1'},"loadFirst")
      },
      contactStart(){
        const tl = gsap.timeline({defaults:{duration:1},onComplete:this.animationComplete})
        !this.from.name?
          tl.delay(0.6)://wanneer pagina voor eerste keer ingeladen wordt
          tl.delay(0.35)
        tl.fromTo('#contact-form',{'transform':'translate(200%, 0)'},{'transform':'translate(0, 0)'},"loadFirst")
        tl.fromTo('#left-contact-side-container',{'transform':'translate(-200%, 0)'},{'transform':'translate(0, 0)'},"loadFirst")
      },
      animationComplete(){
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
    -webkit-transition: all 0.5s linear;
    -moz-transition: all 0.5s linear;
    -o-transition: all 0.5s linear;
    transition: all 0.5s linear;
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

