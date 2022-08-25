<template lang="">
    <ul id="dots-nav">
        <li>
            <RouterLink 
                @mouseover="onMouseOver"
                @mouseleave="onMouseleave"
                to="/" class="dot">
            </RouterLink>
        </li>
        <li>
            <RouterLink 
                @mouseover="onMouseOver"
                @mouseleave="onMouseleave"
                to="/about" class="dot">
            </RouterLink>
        </li>
        <li>
            <RouterLink 
                @mouseover="onMouseOver"
                @mouseleave="onMouseleave"
                to="/projects" class="dot">
                </RouterLink>
        </li>
        <li>
            <RouterLink 
                @mouseover="onMouseOver"
                @mouseleave="onMouseLeave"
                to="/contact" class="dot">
            </RouterLink>
        </li>
  </ul>
  <div id="scroll-indicator-container">
        <div class="scroll-indicator"></div>
        <span>scroll</span>
    </div>
</template>
<script>

export default {
    data(){
        return{
            hideActive:false,
        }
    },
    methods: {
      onMouseOver () {
        this.hideActive=true
      },
      onMouseleave () {
        this.hideActive=false
      }
    },
    // doe met animatie 
    //watch:{
    //     $route (to, from){
    //         this.showScroll = to.name =="home";
    //         console.log(to)
    //     }
    // } 
}
</script>
<style lang="scss">
    #dots-nav{
        display: flex;
        flex-direction: column;
        position: absolute;
        height: 7em;
        transform: translateY(-50%);
        margin-left: 7vw;
        top:50%;
        li{
            height: 1.5rem;
            width: 1.5rem;
            justify-content: center;
            align-items: center;
            display: flex;
            .dot {
                height: 0.7rem;
                width: 0.7rem;
                background-color: $grey;
                border-radius: 50%;
                -webkit-transition: all 0.5s linear;
                -moz-transition: all 0.5s linear;
                -ms-transition: all 0.5s linear;
                -o-transition: all 0.5s linear;
                transition: all 0.5s linear;          
            }
            .dot:hover{
                background-color: $light-pink;
                -webkit-transition: all 0.1s linear;
                -moz-transition: all 0.1s linear;
                -ms-transition: all 0.1s linear;
                -o-transition: all 0.1s linear;
                transition: all 0.1s linear;    
                
            }
            .router-link-active{
                background-color: $pink;
            }
        }
    }

    #scroll-indicator-container{
        transform: translateX(-50%);
        color: $grey;
        position: absolute;
        margin-left:7vw;
        bottom:5vh;
        display: flex;
        flex-direction: column;
        align-items: center;
        span{
            line-height: 2rem;
        }
    }

    .scroll-indicator:before{
        position: absolute;
        left: 50%;
    }
    

    .scroll-indicator{
        position: relative;
        width: 20px;
        height: 40px;
        top: 50%;
        box-shadow: inset 0 0 0 1px $grey;
        border-radius: 20px;
    }

    .scroll-indicator:before{
        content: '';
        width: 6px;
        height: 6px;
        background: $grey;
        margin-left: -3px;
        top: 8px;
        border-radius: 4px;
        animation-duration: 1.5s;
        animation-iteration-count: infinite;
        animation-name: scroll;
    }

    @keyframes scroll{
        0%{
            opacity: 1
        }
        100%{
            opacity: 0;
            transform: translateY(18px);
        }
    }
</style>