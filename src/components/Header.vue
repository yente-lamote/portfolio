<template lang="">
  <header v-bind:class="{'background-color-blue':isOpen}">
    <nav>
        <RouterLink id="home-button" to="/">Yente<span>.</span></RouterLink>
        <button class="hamburger" aria-label="open navigation" v-on:click="handleHamburger" v-bind:class="{open:isOpen}">
          <svg id="burgericon" xmlns="http://www.w3.org/2000/svg" v-bind:class="{open:isOpen}" width="35" height="30">
            <g class="icon">
              <rect class="frstbar" :x="firstX" :y="firstY" width="30" height="4" rx="3" ry="3" fill="#FFFFFF"/>
              <rect class="scndbar" x="2" y="12" width="30" height="4" rx="3" ry="3" fill="#FFFFFF"/>
              <rect class="thrdbar" :x="thirdX" :y="thirdY" width="30" height="4" rx="3" ry="3" fill="#FFFFFF"/>
            </g>
          </svg>
        </button>        
        <div id="nav-list" v-bind:class="{open:isOpen}">
          <ul id="nav-left">
            <li>
              <RouterLink to="/projects" class="page-link">Projects</RouterLink>
              <span class="dot"></span>
            </li>
            <li>
              <RouterLink to="/about" class="page-link">About</RouterLink>
              <span class="dot"></span>
            </li>
            <li>
              <RouterLink to="/contact" class="page-link">Contact</RouterLink>
            </li>
          </ul>
          <div>
            <a href="/resume.pdf" class="resume" target="_blank">Resume</a>
          </div>
        </div>
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
  .background-color-blue{
    background-color: $blue-100;
  }
  header{
    position: fixed;
    width: 100%;
    z-index:2;
    nav{
      width: 80vw;
      margin: auto;
      margin:auto;
      display: flex;
      flex-wrap: wrap;
      vertical-align: center;
      #home-button{
        font-size: 2.4rem;
        color: $white;
        font-weight: bold;
        padding:0.75rem 0;
        margin-right:1.5rem;
        span{
          color: $pink;
          border-radius: 25%;
        }
      }
      #home-button:hover{
        margin-top:0px;
        color: $grey;
      }
      .resume{
        background-color: $pink;
        color:white;
        margin-left: 1rem;
        padding:0.7rem 1.5rem;
        margin-top:auto;
        margin-bottom: auto;
        border-radius: 10px;
        font-weight: 600;
      }
      .resume:hover{
        background-color: $light-pink;
        transform: translateY(-2px);
        
      }
      #nav-list{
        justify-content: space-between;
        display: flex;
        overflow: hidden;
        transition: max-height 0.2s  linear;
        margin-top:8px;
        flex-grow: 1;
        #nav-left{
          display: flex;
        }
        li{
          display: flex;
          flex-direction: column;
          justify-content: center;
          position: relative;
          padding: 0 0.3rem;
          .router-link-active{
            color:$white;
          }
          a{
            border-radius: 10px;
            font-size: 1em;
            padding:0.75rem 1.5rem;
            color: $grey;
            font-weight: 600;
            -webkit-transition: all 0.1s linear;
            -moz-transition: all 0.1s linear;
            -ms-transition: all 0.1s linear;
            -o-transition: all 0.1s linear;
            transition: all 0.1s linear;  
          }
          a:hover{
            margin-top: -2px;
            color:$white;
          }
          .page-link:hover::after{
            visibility: visible;
            bottom: 7px;
          }
          .page-link::after {
            content: '';
            z-index: 4;
            height: 0.3rem;
            width: 0.3rem;
            background-color: $pink;
            color: $pink;
            border-radius: 50%;
            visibility: hidden;
            position: absolute;
            bottom: 0px;
            left: 50%;
            -webkit-transition: all 0.1s linear;
            -moz-transition: all 0.1s linear;
            -ms-transition: all 0.1s linear;
            -o-transition: all 0.1s linear;
            transition: all 0.1s linear;  
          }
        }
        div{
          display: flex;
        }
      }     
      }
      
      .hamburger{
        display: none;
        text-align: center;
        margin-right: 1em;
        margin-top: auto;
        margin-bottom: auto;
        margin-left: auto;
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
  @media screen and (max-width: 1650px) {
    header{
      nav{
        width: 90%;
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
      padding: 0;
      margin-top: 0.5rem;
      padding-bottom: 0.6rem;
      margin-top:0;
      nav{
        width: 100;
        padding-left: 5%;
        padding-right: 5%;
        #nav-list{
          flex-basis: 100%;
          flex-direction: column;
          margin-top: -5px;
          margin-left: -0.5rem;
          max-height: 0px;
          #nav-left{
            flex-direction: column;
            li{
              a{
                padding: 0.75rem 1.5rem;
              }

              .page-link::after{
                display: none;
              }
              
            }
          }
          .resume{
            background-color: $pink !important;
            margin-bottom: 15px;
            margin-left: 1.5em;
            margin-top: 0.5em;
          }
        }
        a:hover{
            margin-top: 0 !important;
        }
      }
    }
    
    .open{
      max-height: 200px !important;
    }
    header{
      .hamburger{
        display: flex;
        margin-right: 0;
      }
      .dot{
      display: none;
      }
      background-color: transparent;
    }
    
    
    #home-button{
      font-size: 2rem !important;
    }
    a{
      font-size: 1rem !important;
    }
  }
</style>