<template lang="">
    <header>
    <nav>
        <RouterLink class="home" to="/">Yente<span>.</span></RouterLink>
        <button class="hamburger" v-on:click="handleHamburger" v-bind:class="{open:isOpen}">
          <svg id="burgericon" xmlns="http://www.w3.org/2000/svg" v-bind:class="{open:isOpen}" width="35" height="30">
            <g class="icon">
              <rect class="frstbar" :x="firstX" :y="firstY" width="30" height="4" rx="3" ry="3" fill="#414141"/>
              <rect class="scndbar" x="2" y="12" width="30" height="4" rx="3" ry="3" fill="#414141"/>
              <rect class="thrdbar" :x="thirdX" :y="thirdY" width="30" height="4" rx="3" ry="3" fill="#414141"/>
            </g>
          </svg>
        </button>        
        <ul v-bind:class="{open:isOpen}">
          <li>
            <RouterLink to="/about">about</RouterLink>
            <span class="dot"></span>
          </li>
          <li>
            <RouterLink to="/projects">projects</RouterLink>
            <span class="dot"></span>
          </li>
          <li>
            <RouterLink to="/contact">contact</RouterLink>
            <span class="dot"></span>
          </li>
          <li>
            <RouterLink class="resume" to="/resume">resume</RouterLink>
          </li>
        </ul>
    </nav>
  </header>
</template>
<script>
export default{
  data(){
    return{
        isOpen: false,
        firstX:2,
        firstY:3,
        thirdX:2,
        thirdY:21,
    }
  },
  methods:{
    handleHamburger:function(){
        if(!this.isOpen){
            this.firstX=5;
            this.firstY=0;
            this.thirdX=-16;
            this.thirdY=19;
        }else{
            this.firstX=2;
            this.firstY=3;
            this.thirdX=2;
            this.thirdY=21;
        }
        this.isOpen = !this.isOpen
    }
  }
}
</script>
<style lang="scss">
  header{
    width: 80vw;
    margin: auto;
    padding:1rem;
    nav{
      margin:auto;
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      vertical-align: center;
      .home{
        font-size: 2.4rem;
        margin:0;
        color: $dark-blue;
        font-weight: bold;
        span{
          color: $blue;
          border-radius: 25%;
        }
      }
      .home:hover{
        margin-top:0px;
      }
      .resume{
        background-color: $blue;
        color:white;
        -webkit-transition: background-color 0.1s linear;
        -ms-transition: background-color 0.1s linear;
        transition: background-color 0.1s linear;
        margin-left: 1rem;
        padding:0.7rem 1.5rem;
      }
      .resume:hover{
        color:white;
        background-color:#4d78ff;
        margin-top:0px;
      }
      li{
        display: flex;
        flex-direction: column;
        justify-content: center;
        position: relative;
        margin-left: 1rem;
        padding: 0 0.3rem;
        .dot {
          height: 0.3rem;
          width: 0.3rem;
          background-color: $blue;
          border-radius: 49%;
          position: absolute;
          bottom: 0px;
          left: 50%;
          visibility: hidden;
          -webkit-transition: all 0.1s linear;
          -moz-transition: all 0.1s linear;
          -ms-transition: all 0.1s linear;
          -o-transition: all 0.1s linear;
          transition: all 0.1s linear;  
        }
      }
      a{
        border-radius: 10px;
        font-size: 1em;
        padding:0.7rem 1rem;
        color: $grey;
        font-weight: 600;
      }
      a:hover{
        margin-top: -2px;
        color:$dark-blue;
      }
      a:hover + .dot{
        visibility: visible;
        bottom: 7px;
      }
      ul{
        display: flex;
        overflow: hidden;
        transition: max-height 0.2s  linear;
        margin-top:8px;
      }
      .hamburger{
        display: none;
        text-align: center;
        margin-right: 1em;
        margin-top: auto;
        margin-bottom: auto;
        background: none;
        border: none;
        padding: 0.5rem;
        cursor: pointer;
        font: inherit;
      }
      #burgericon{
        margin-top: 8px;
        height: auto;
      }
      #burgericon.open .frstbar {
        -webkit-transform: rotate(45deg);
        -ms-transform: rotate(45deg);
        transform: rotate(45deg);
      }
      #burgericon.open .thrdbar {
        -webkit-transform: rotate(-45deg);
        -ms-transform: rotate(-45deg);
        transform: rotate(-45deg);
      }
      #burgericon.open .scndbar { 
        width: 0; 
        opacity: 0; 
      }
      .frstbar, .scndbar, .thrdbar {
        -webkit-transition: all 0.35s linear;
        -moz-transition: all 0.35s linear;
        -o-transition: all 0.35s linear;
        transition: all 0.35s linear;
      }
    }
  }

  @media screen and (max-width: 1024px) {
    li{
      margin-left: 0 !important;
    }
  }

  @media screen and (max-width: 800px) {
    header{
      width: 100%;
      padding: 0 0.5rem;
      margin-top: 0.5rem;
      padding-bottom: 0.6rem;
    }
    ul{
      flex-basis: 100%;
      flex-direction: column;
      margin-left: 1rem !important;
      max-height: 0px;
      li{
        width: 88vw;
      }
    }
    .open{
      max-height: 200px;
    }
    .hamburger{
      display: flex !important;
    }
    .resume{
      background-color: white !important;
      color: $dark-blue !important;
    }
    .dot{
      display: none;
    }
    a:hover{
        margin-top: 0 !important;
    }
    .home{
      font-size: 2rem !important;
    }
    a{
      font-size: 1rem !important;
    }
  }
</style>