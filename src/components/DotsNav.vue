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
</template>
<script>

export default {
    data(){
        return{
        }
    }, 
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
    }

    @media screen and (max-width: 500px) {
        #dots-nav{
            transform: translateY(-50%) translateX(-50%);
        }

    }
</style>