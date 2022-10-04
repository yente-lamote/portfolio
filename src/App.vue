<script setup>
import Header from "./components/Header.vue"
import HomeView from "./views/HomeView.vue";
import TopRightBars from "./components/svg's/TopRightBars.vue";
import DotsNav from './components/DotsNav.vue';
import ProjectsView from "./views/ProjectsView.vue";
import router from "./router";
import Contact from "./views/Contact.vue";
import AboutView from "./views/AboutView.vue";
</script>
<template>
  <TopRightBars></TopRightBars>
  <DotsNav></DotsNav>
  <Header></Header>
  <main>
    <HomeView class="page" :style="{'transform':`translateY(-${translateY}px)`}"></HomeView>
    <ProjectsView class="page" :style="{'transform':`translateY(-${translateY}px)`}"></ProjectsView>
    <AboutView class="page" :style="{'transform':`translateY(-${translateY}px)`}"></AboutView>
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
          const tl = gsap.timeline({defaults:{duration:0.5,ease: Power2.easeIn}})
          tl.delay(0.5)
          tl.add("start")
          tl.fromTo('#profile-picture',{'transform':'scale(0.6) translateY(-40%)'},{'transform':'scale(1) translateY(0)',duration:0.7, ease: Sine.easeOut},"start")
          tl.fromTo("#about nav ul li",{"transform":"translateX(40px)","opacity":0.001},{"transform":"translateX(0)","opacity":1},"start")
          tl.fromTo(".tab",{"transform":"translateY(20px)","opacity":0.001},{"transform":"translateY(0)","opacity":1,delay:0.1},"start")
          tl.fromTo("#about .social-links",{"transform":"translateX(10px)","opacity":0.001},{"transform":"translateX(0)","opacity":1,delay:0.2},"start")
        }
        await new Promise(resolve => setTimeout(resolve, 1400));
        this.animationComplete();
      },
      homeEnter(){
        const tl = gsap.timeline({defaults:{duration:0.7,delay:0},onComplete:this.animationComplete})
        /*!this.from.name?
          tl.delay(0.6)://wanneer pagina voor eerste keer ingeladen wordt
          tl.delay(0.6)*/
        tl.delay(0.6)
        tl.add("start")
        tl.fromTo('#scroll-indicator-container',{'transform':'translateY(100vh) translateX(-50%)','display':'none','opacity':0.001},{'display':'flex','transform':'translateY(0) translateX(-50%)','opacity':1},'start')
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

      contactEnter(){
        const tlHide = gsap.timeline({defaults:{duration:0}})

        const tl = gsap.timeline({defaults:{duration:0.4,ease: Power1.easeIn},onComplete:this.animationComplete})
        tl.delay(0.6)
        tl.add("start")
        tl.fromTo('#name-container',{'transform':'translateY(30px)','opacity':'0.001'},{'transform':'translateY(0)','opacity':'1',delay:0.2},"start")
        tl.fromTo('#email-container',{'transform':'translateY(30px)','opacity':'0.001'},{'transform':'translateY(0)','opacity':'1', delay:0.3},"start")
        tl.fromTo('#message-container',{'transform':'translateY(30px)','opacity':'0.001'},{'transform':'translateY(0)','opacity':'1', delay:0.4},"start")
        tl.fromTo('#submit-container',{'transform':'translateY(30px)','opacity':'0.001'},{'transform':'translateY(0)','opacity':'1', delay:0.5},"start")

        tl.fromTo('#contact-info div h1',{'opacity':'0.001'},{'opacity':'1'},"start")
        tl.fromTo('.contact-side-container p',{'transform':'translateY(5px)','opacity':'0.001'},{'transform':'translateY(0)','opacity':'1',delay:0.3},"start")
        tl.fromTo('#arrow, .social-links',{'opacity':'0.001'},{'opacity':'1',delay:0.5},"start")

      },
      projectEnter(){
        //less lagier than using fromto
        const tlHide = gsap.timeline({defaults:{duration:0}})
        tlHide.add("start")
        tlHide.to('#mockups-desktop, #projects-mobile img',{'transform':'scale(0.4) translateY(-60%)'},"start")
        tlHide.to('#projects-mobile h1',{'transform':'translateX(-140%)'},"start")
        tlHide.to('#projects-desktop h1',{'autoAlpha':'0'},"start",)
        tlHide.to('#projects-desktop h2',{'autoAlpha':'0', 'transform':'translateY(20px)'},"start")
        tlHide.to('#lead-project-main-info',{'autoAlpha':'0', 'transform':'translateY(20px)'},"start")
        tlHide.to('#lead-project-api-info',{'autoAlpha':'0', 'transform':'translateY(20px)'},"start")
        tlHide.to('#projects-desktop #technologies',{'opacity':'0', 'transform':'translateY(20px)'},"start")
        tlHide.to('#projects-desktop .button-full',{'opacity':'0', 'transform':'translateY(35px)'},"start")
        tlHide.to('#projects-desktop .button-border',{'opacity':'0', 'transform':'translateY(35px)'},"start")
        tlHide.to('#projects-mobile .button-full',{'opacity':'0', 'transform':'translateY(10px)'},"start")
        tlHide.to('#projects-mobile .button-border',{'opacity':'0', 'transform':'translateY(10px)'},"start")

        const tl = gsap.timeline({defaults:{duration:0.4},onComplete:this.animationComplete})
        tl.delay(0.3)
        tl.add("start")
        tl.to('#mockups-desktop, #projects-mobile img',{'transform':'scale(1) translateY(0)',ease: Sine.easeOut,duration:0.7},"start")
        tl.to('#projects-desktop h1',{'autoAlpha':'1', delay:0.3},"start",)
        tl.to('#projects-desktop h2',{'autoAlpha':'1', 'transform':'translateY(0)',delay:0.4},"start")
        tl.to('#lead-project-main-info',{'autoAlpha':'1', 'transform':'translateY(0)', delay:0.5},"start")
        tl.to('#lead-project-api-info',{'autoAlpha':'1', 'transform':'translateY(0)', delay:0.6},"start")
        tl.to('#projects-desktop #technologies',{'opacity':'1', 'transform':'translateY(0)', delay:0.7},"start")
        tl.to('#projects-desktop .button-full',{'opacity':'1', 'transform':'translateY(0)',duration:0.5,delay:0.8},"start")
        tl.to('#projects-desktop .button-border',{'opacity':'1', 'transform':'translateY(0)',duration:0.6,delay:0.9},"start")
        tl.to('#projects-mobile h1',{'transform':'translateX(0)', duration:0.7, delay:0.2},"start")
        tl.to('#projects-mobile .button-full',{'opacity':'1', 'transform':'translateY(0)',delay:0.4},"start")
        tl.to('#projects-mobile .button-border',{'opacity':'1', 'transform':'translateY(0)',delay:0.5},"start")
      },
      projectLeave(){
        const tl = gsap.timeline({defaults:{duration:0.6}})
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
      setCurrentPage(page){
        this.currentPage=page
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
          if ( xDiff > 0) {//right swipe
            if(this.currentPage==2||this.currentPage==3){
              this.handleScrollDown()
            }
          } else {//left
            if(this.currentPage==3||this.currentPage==4){
              this.handleScrollUp()
            }
          }
        }                       
        else {
            if ( yDiff > 0 ) {//down
              if(this.pages[this.currentPage].pageTranslate==2){
                this.setCurrentPage(5)
              }else{
                this.handleScrollDown()
              }
            } else { //up
              if(this.pages[this.currentPage].pageTranslate==2){
                this.setCurrentPage(1)
              }else if(this.pages[this.currentPage].pageTranslate==3){
                this.setCurrentPage(2)
              }else{
                this.handleScrollUp()
              }
            }                 
        }
        router.push({name:this.pages[this.currentPage].name})                                                
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
    -moz-transform: scale(1, 1);
    -o-transform: scale(1, 1);
    -webkit-transform: scale(1, 1);
    -ms-transform: scale(1, 1);
  }
  25% {
    transform: scale(1, 1.5);
    -moz-transform: scale(1, 1.5);
    -o-transform: scale(1, 1.5);
    -webkit-transform: scale(1, 1.5);
    -ms-transform: scale(1, 1.5);
  }
  50% {
    transform: scale(1, 0.67);
    -moz-transform: scale(1, 0.67);
    -o-transform: scale(1, 0.67);
    -webkit-transform: scale(1, 0.67);
    -ms-transform: scale(1, 0.67);
  }
  75% {
    transform: scale(1, 1);
    -moz-transform: scale(1, 1);
    -o-transform: scale(1, 1);
    -webkit-transform: scale(1, 1);
    -ms-transform: scale(1, 1);
  }
  100% {
    transform: scale(1, 1);
    -moz-transform: scale(1, 1);
    -o-transform: scale(1, 1);
    -webkit-transform: scale(1, 1);
    -ms-transform: scale(1, 1);
  }
}

@keyframes dotElastic {
  0% {
    transform: scale(1, 1);
    -moz-transform: scale(1, 1);
    -o-transform: scale(1, 1);
    -webkit-transform: scale(1, 1);
    -ms-transform: scale(1, 1);
  }
  25% {
    transform: scale(1, 1);
    -moz-transform: scale(1, 1);
    -o-transform: scale(1, 1);
    -webkit-transform: scale(1, 1);
    -ms-transform: scale(1, 1);
  }
  50% {
    transform: scale(1, 1.5);
    -moz-transform: scale(1, 1.5);
    -o-transform: scale(1, 1.5);
    -webkit-transform: scale(1, 1.5);
    -ms-transform: scale(1, 1.5);
  }
  75% {
    transform: scale(1, 1);
    -moz-transform:  scale(1, 1);
    -o-transform: scale(1, 1);
    -webkit-transform: scale(1, 1);
    -ms-transform: scale(1, 1);
  }
  100% {
    transform: scale(1, 1);
    -moz-transform:  scale(1, 1);
    -o-transform: scale(1, 1);
    -webkit-transform: scale(1, 1);
    -ms-transform: scale(1, 1);
  }
}

@keyframes dotElasticAfter {
  0% {
    transform: scale(1, 1);
    -moz-transform: scale(1, 1);
    -o-transform: scale(1, 1);
    -webkit-transform: scale(1, 1);
    -ms-transform: scale(1, 1);
  }
  25% {
    transform: scale(1, 1);
    -moz-transform: scale(1, 1);
    -o-transform: scale(1, 1);
    -webkit-transform: scale(1, 1);
    -ms-transform: scale(1, 1);
  }
  50% {
    transform: scale(1, 0.67);
    -moz-transform: scale(1, 0.67);
    -o-transform: scale(1, 0.67);
    -webkit-transform: scale(1, 0.67);
    -ms-transform: scale(1, 0.67);
  }
  75% {
    transform: scale(1, 1.5);
    -moz-transform: scale(1, 1.5);
    -o-transform: scale(1, 1.5);
    -webkit-transform: scale(1, 1.5);
    -ms-transform: scale(1, 1.5);
  }
  100% {
    transform: scale(1, 1);
    -moz-transform: scale(1, 1);
    -o-transform: scale(1, 1);
    -webkit-transform: scale(1, 1);
    -ms-transform: scale(1, 1);

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

    -webkit-transition: all 1000ms cubic-bezier(0.645, 0.045, 0.355, 1) 0s;
    -webkit-transition-property: all;
    -webkit-transition-duration: 1000ms;
    -webkit-transition-timing-function: cubic-bezier(0.645, 0.045, 0.355, 1);
    -webkit-transition-delay: 0s;

    -moz-transition: all 1000ms cubic-bezier(0.645, 0.045, 0.355, 1) 0s;
    -moz-transition-property: all;
    -moz-transition-duration: 1000ms;
    -moz-transition-timing-function: cubic-bezier(0.645, 0.045, 0.355, 1);
    -moz-transition-delay: 0s;

    -ms-transition: all 1000ms cubic-bezier(0.645, 0.045, 0.355, 1) 0s;
    -ms-transition-property: all;
    -ms-transition-duration: 1000ms;
    -ms-transition-timing-function: cubic-bezier(0.645, 0.045, 0.355, 1);
    -ms-transition-delay: 0s;

    -o-transition: all 1000ms cubic-bezier(0.645, 0.045, 0.355, 1) 0s;
    -o-transition-property: all;
    -o-transition-duration: 1000ms;
    -o-transition-timing-function: cubic-bezier(0.645, 0.045, 0.355, 1);
    -o-transition-delay: 0s;
    
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

