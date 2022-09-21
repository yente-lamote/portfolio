<template>
    <section id="home">
        <div class="content-container">
            <aside id="face-wrapper">
                <Face></Face>
            </aside>
            <div id="home-title">
                <h1 id="desktop-h1">
                    A Full Stack Developer<br>
                    <span>
                        With a passion for <br> solving problems <br> with code
                    </span>
                </h1>
                <div id="mobile-h1">
                    <h1>
                        Yente Lamote<br>
                        <span>
                            Full Stack Developer
                        </span>
                    </h1>
                </div>
            </div>
        </div>
    </section>
</template>
<script>
import Face from '../components/Face.vue';

export default {
    components: { Face },
    mounted(){

    },
}

</script>
<style lang="scss">
    #home .content-container{
        flex-direction: row-reverse;
        justify-content: space-between;
    }
    #home-title{
        margin: auto 0;
        h1{
            color: $grey;
            font-size: 2.5rem;
            font-weight: 300;
            span{
                color:$white;
                font-size:4rem;
                font-weight: 500;
            }
        }
        #mobile-h1{
            display:none;
        }
    }
    #face-wrapper{
        width:53vh;
        margin-right: 6em;
        right:0;
    }

    @media screen and (max-width: 1650px) {
        #home-title h1{
            font-size:2.2rem;
            span{
                font-size: 3.8rem;
            }
        }
        #face-wrapper{
            margin-right: 4em;
        }
    }

    @media screen and (max-width: 1300px) {
        #home-title h1{
            font-size:2rem;
            span{
                font-size: 3.5rem;
            }
        }
        #face-wrapper{
            margin-right: 2em;
        }
    }
    @media screen and (max-width: 950px) and (min-width:500px) {
        #home-title h1{
            font-size:1.5rem;
            span{
                font-size: 2.7rem;
            }
        }
        #home .content-container{
            flex-direction: column;
            height: 70%;
            justify-content: space-between;
        }
        #face-wrapper{
            width: 50vw;
            margin-left: auto;
            margin-right:auto !important;
            transform:none;
            top:10vh;
        }
        #home-title{
            display: flex;
            justify-content: center;
            transform: none;
            top:15vh;
            transform: translateX(-50%);
            left:50%
        }
    }
    @media screen and (max-width: 500px) {
        #home-title{
            bottom:0;
            position: relative;
            z-index: 3;
            top:auto;
            transform: none;
            #desktop-h1{
                display:none;
            }
            #mobile-h1{
                display:flex;
                margin-bottom: 13vh;                
                h1{
                margin:auto;
                margin-left:8vw;
                width: 100%;
                font-size:2rem;
                line-height: 1.8rem;
                font-weight: 600;
                color:$white;
                    span{
                        font-size:1rem;
                        color:$grey;
                        font-weight:normal;
                    }
                }   
            }
        }
        header{
            background-color: none;
        }
        main{
            overflow: visible;
        }
        #face-wrapper{
            position:relative;
            width: 65vh;
            margin-left:15vw;
            transform:none;
            top: 0;
        }
        #home .content-container{
            flex-direction: column;
        }
    }
</style>