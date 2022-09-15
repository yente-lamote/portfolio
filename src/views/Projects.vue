<template>
    <section id="projects">
        <div class="content-container">
            <article>
                <h1>My projects</h1>
                <p>Over the last couple of years I have made several projects. One of those projects Is a web application that stores leads centrally. My lead-project allows users to keep track 
                    of new leads with a couple dashboards. New leads are added with API request. I've also made a Drupal module that sends a new API request to the server whenever a form is submitted.
                </p>
                <a class="highlight-button" href="#">View Lead-project</a>
                <a href="#">See all projects</a>
            </article>
            <Laptop id="laptop"></Laptop>
        </div>
    </section>
</template>
<script>
import Laptop from "../components/svg's/Laptop.vue";

export default {
    components: { Laptop }
}
</script>
<style lang="scss">
    #projects{
        overflow: visible;
    }
    #laptop{
        position: absolute;
        width: 60vw;
        right:-25%;
        top:50%;
        transform: translateY(-50%);
    }
    #projects{
        .content-container{
            color:$white;
            article{
                width: 40%;
                h1{
                font-size: 4em;
                }
                p{
                    margin-top:2rem;
                    font-size:1.2em;
                    line-height: 1.3;
                    color: $grey;
                }
                a{
                    margin-top: 2em;
                    padding: 0.8em 1.5em;
                    display: inline-block;
                    color:white;
                    border-radius: 10px;
                    border:1px solid $white;
                    margin-right: 3em;
                    font-weight: 600;
                }
                .highlight-button{
                    background-color: $white;
                    color: $blue-400;
                }
            }
            
        }
    }
</style>