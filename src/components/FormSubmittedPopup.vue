<template lang="">
    <div id="popup-container">
        <div class="popup" v-if="!showError">
            <p class="title">Thank you</p>
            <p>Your message has been sent!</p>
            <p>I will try to get back to you.</p>
            <a @click="goBackToSite">Back to site</a>
        </div>
        <div class="popup" v-if="showError">
            <p class="title">Something went wrong</p>
            <p>Please try again or use another method to contact me.</p>
            <a @click="goBackToSite">Back to site</a>
        </div>
    </div>

</template>
<script>
export default {
    props: ['showError'],
    methods:{
        goBackToSite(){
            this.$emit('showPopup', false)
        }
    },
    mounted(){
        document.addEventListener("click",(e)=>{
            if(e.target.closest('.popup')==null){
                this.goBackToSite()
            }
        })
    }
}
</script>
<style lang="scss">
    #contact{
        overflow: visible;
    }
    #popup-container{
        background-color: rgba($color: #000000, $alpha: 0.3);
        height: 100vh;
        position: absolute;
        left: -20%;
        right: -20%;
        top: 0;
    }
    .popup{
        padding: 2.5em 5em;
        background-color: $white;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translateX(-50%) translateY(-50%);
        p{
            text-align: center;
            color: $grey;
            margin-bottom: 0.2em;
        }
        .title{
            font-size: 2em;
            color: $blue-600;
            margin-bottom: 0.5em;
        }
        a{
            display: block;
            width: 100%;
            background-color: $blue-200;
            color: white;
            text-align: center;
            border-radius: 20px;
            padding: 0.7em;
            margin-top: 1.5em;
        }
        a:hover{
            cursor: pointer;
        }
    }
    @media screen and (max-width: 830px){
        .popup{
            padding: 2.5em;
            width: 75%;
            box-sizing: border-box;
        }

    }
</style>