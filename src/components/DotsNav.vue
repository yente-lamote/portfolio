<template lang="">
    <ul id="dots-nav">
        <li>
            <RouterLink 
                to="/" class="dot">
            </RouterLink>
        </li>
        <li>
            <RouterLink 
                to="/about" class="dot">
            </RouterLink>
        </li>
        <li>
            <RouterLink 
                to="/projects" class="dot">
                </RouterLink>
        </li>
        <li>
            <RouterLink 
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
        position: fixed;
        height: 7em;
        transform: translateY(-50%);
        margin-left: 7vw;
        top:50%;
        z-index: 1;
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
                background-color: $pink;
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
        position: fixed;
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

    @media screen and (max-width: 1650px) and (min-width:800px) {
        #dots-nav{
            bottom:5vh;
            flex-direction: row;
            transform: translateX(-50%);
            left:50vw;
            margin-left:0;
            top:auto;
            height: auto;
        }
        #scroll-indicator-container{
            margin-left:5vw;
        }
    }
    @media screen and (max-width: 500px) {
        #scroll-indicator-container{
            display: none;
        }
        #dots-nav{
            transform: translateY(-50%) translateX(-50%);
        }

    }
</style>