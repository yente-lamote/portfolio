<template lang="">
    <ul id="dots-nav">
        <li>
            <RouterLink to="/" class="dot active" ></RouterLink>
        </li>
        <li>
            <RouterLink to="/about" class="dot"></RouterLink>
        </li>
        <li>
            <RouterLink to="/projects" class="dot"></RouterLink>
        </li>
        <li>
            <RouterLink to="/contact" class="dot"></RouterLink>
        </li>
  </ul>
</template>
<script>
export default {
    
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
                -webkit-transition: all 0.1s linear;
                -moz-transition: all 0.1s linear;
                -ms-transition: all 0.1s linear;
                -o-transition: all 0.1s linear;
                transition: all 0.1s linear;          
            }
            .dot:hover{
                background-color: $light-pink;
                height: 1rem;
                width: 1rem;
            }
            .active{
                background-color: $pink;
            }
        }
        
    }
</style>