<template lang="">
    <div id="homeViewcontainer">
        <section>
            <h1>
                A Full Stack Developer<br>
                <span>
                    With a passion for <br> solving problems <br> with code
                </span>
            </h1>
        </section>
        <aside id="face-wrapper">
            <Face></Face>
        </aside>
    </div>
</template>
<script>
import Face from '../components/Face.vue';

export default {
    components: { Face },
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
    @media screen and (max-width: 950px) {
        section h1{
            font-size:1.5rem;
            span{
                font-size: 2.7rem;
            }
        }
    }
    @media screen and (max-width: 800px) {
        section{ 
            margin-top: 4em;
            h1{
                margin:auto;
                width: 80vw;
                font-size:1.5rem;
                color:$white;
                font-weight: 400;
                span{
                    font-size: 1.5rem;
                    color:$grey;
                    font-weight:normal;
                }
            }
        }
        section{
            position: relative;
            top:auto;
            transform: none;
        }
        #face-wrapper{
            position:relative;
            width: 70vw;
            margin:auto;
            transform:none;
        }
        #homeViewcontainer{
            margin-top:5em;
            display: flex;
            flex-direction: column-reverse;
        }
    }
</style>