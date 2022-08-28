<template>
    <div id="home-view-container">
        <aside id="face-wrapper">
            <Face></Face>
        </aside>
        <section id="info">
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
        </section>
    </div>
</template>
<script>
import Face from '../components/Face.vue';

export default {
    components: { Face },
    mounted(){
        const tl = gsap.timeline({defaults:{duration:0.9}})
        tl.delay(0.4)
        tl.add("home")
        tl.fromTo('#info',{'margin-left':'-100%',opacity:0},{'margin-left':'0px',opacity:1, ease:Power2.easeOut,},"home")
        tl.fromTo('#face-wrapper',{'right':'-100%',opacity:0},{'right':'0',opacity:1, ease:Power2.easeOut},"home")
        tl.fromTo('#top-right-bars',{'margin-top':'-100%',"margin-right":"-100%"},{'margin-top':'0',"margin-right":"0", ease:Power2.easeOut, duration:1.3},"home")
    },
}

</script>
<style lang="scss">
    section{
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
    @media screen and (max-width: 1650px) {
        section h1{
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
        section h1{
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
        section h1{
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
        section{
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
        section{
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
    }
</style>