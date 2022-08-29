<template>
    <section>
        <div id="home-view-container">
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
        <div id="scroll-indicator-container">
            <div class="scroll-indicator"></div>
        <span>scroll</span>
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
    #home-title{
        position: absolute;
        top:50%;
        transform: translateY(-50%);
        h1{
            color: $grey;
            font-size: 2.5rem;
            font-weight: 300;
            span{
                color:$white;
                font-size:4.5rem;
                font-weight: 500;
            }
        }
        #mobile-h1{
            display:none;
        }
    }
    #face-wrapper{
        position: absolute;
        top:50%;
        transform: translateY(-50%);
        width:53vh;
        margin-right: 6em;
        right:0;
    }

    #scroll-indicator-container{
        color: $grey;
        position: fixed;
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
        #face-wrapper{
            position:relative;
            width: 50vw;
            margin-left: auto;
            margin-right:auto;
            transform:none;
            top:10vh;
        }
        #home-title{
            display: flex;
            justify-content: center;
            position: relative;
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
        #home-view-container{
            display: flex;
            flex-direction: column;
            justify-content: space-between;
        }
        #scroll-indicator-container{
            display: none;
        }
    }
</style>