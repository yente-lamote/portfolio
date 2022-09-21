<template>
    <section id="projects">
        <div class="content-container">
            <div id="projects-desktop">
                <article>
                    <div>
                    <h1>Featured Project</h1>
                    <div class="subtitle">
                        <h2>Lead Project</h2>
                    </div>
                    <p>
                        Lead Project is a web application that visualizes a company's leads.
                        It allows users to keep track of their leads with various dashboards.
                        Users are also able to change leads and view a leads history. On top
                        of that the application has role-based access control. So only
                        employees with a certain role can edit the leads.
                    </p>
                    <p>
                        New leads can be added with API requests. For Drupal I've 
                        made a module that automatically sends an API request to the 
                        server whenever a form with lead data is submitted. 
                    </p>
                    <div id="technologies">
                        <div id="icons">
                            <div class="icon">
                                <img id="laravel" src="@/assets/images/icons/laravel.png" alt="laravel logo"/>
                                <span class="tooltip">Laravel</span>
                            </div>
                            <div class="icon">
                                <img id="vue" src="@/assets/images/icons/vue.js.png" alt="vue.js logo"/>
                                <span class="tooltip">Vue.js</span>
                            </div>
                            <div class="icon">
                                <img id="tailwindcss" src="@/assets/images/icons/Tailwindcss.png" alt="Tailwind css logo"/>
                                <span class="tooltip">Tailwind CSS</span>
                            </div>
                            <div class="icon">
                                <img id="meilisearch" src="@/assets/images/icons/meilisearch.png" alt="meilisearch logo"/>
                                <span class="tooltip">Meilisearch</span>
                            </div>
                            <div class="icon">
                                <img id="drupal" src="@/assets/images/icons/drupal.png" alt="drupal logo"/>
                                <span class="tooltip">Drupal</span>
                            </div>
                            <div class="icon">
                                <img id="amazon-lightsail" src="@/assets/images/icons/amazon-lightsail.svg" alt="amazon lightsail logo"/>
                                <span class="tooltip">Amazon Lightsail</span>
                            </div>
                        </div>
                    </div>
                    <div class="buttons">
                        <a class="button-full" href="https://lead-project.yentelamote.be">View Lead-project</a>
                        <a class="button-border" href="#">See all projects</a>
                    </div>
                    </div>
                </article>
                <div id="mockups-desktop">
                    <img src="@/assets/images/phone-mockups-desktop-version.png" alt="phone mockups"/>
                </div>
                <!-- <Laptop id="laptop"></Laptop> -->
            </div>
            <div id="projects-mobile">
                <img src="@/assets/images/phone-mockups-mobile-version.png" alt="phone mockups"/>
                <div class="container">
                    <h1>My projects</h1>
                    <div class="buttons">
                        <a href="https://lead-project.yentelamote.be" class="button-full">Lead project</a>
                        <a href="#" class="button-border">All projects</a>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>
<script>
import Laptop from "../components/svg's/Laptop.vue";

export default {
    components: { Laptop },
    data:()=>{
        return{
            selectedTechnology:""
        }
    },
    methods:{
        handleImageHover:(e)=>{
            const tl = gsap.timeline({defaults:{duration:0.7,ease: Power1.easeIn},onComplete:this.animationComplete})
            tl.fromTo('#contact-form',{'transform':'translate(200%, 0)'},{'transform':'translate(0, 0)'},"loadFirst")
        }
    }
}
</script>
<style lang="scss">
    .button-full{
        color: $blue-400;
        background-color: $white; 
    }
    .button-border{
        margin-left: 1em;
        color:$white;
    }

    #projects-mobile{
        display: none;
    }
    #projects{
        overflow: visible;
        a{
            padding: 0.8em 1.5em;
            display: inline-block;
            border-radius: 10px;
            border:1px solid $white;
            font-weight: 600;
        }
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
            #projects-desktop{
                display: flex;
                width: 65vw;
                margin: auto;
            }
            article{
                width: 44%;
                margin-right:auto;
                display: flex;
                align-items: center;
                h1{
                    font-size: 3em;
                    margin-bottom: 0.4em;
                    font-weight: 500;
                }
                .subtitle{
                    display: flex;
                    align-items: center;
                    padding-bottom:0.9rem;
                    h2{
                        font-size: 2em;
                        display: inline;
                        font-weight: normal;
                    }
                    span{
                        font-size: 1.4em;
                        margin-left: 5px;
                        color: $pink;
                        margin-top: 3px;
                        font-weight: 200;
                    }
                }
                
                p{
                    padding-bottom:0.9rem;
                    font-size:1.1em;
                    line-height: 1.6;
                    color: $grey;
                }
                #technologies{
                    margin-top: 2em;
                    margin-bottom: 2em;
                    #icons{
                        display:flex;
                        flex-direction: row;
                        align-items: center;
                        height: 60px;
                        .icon{
                            width: 60px;
                            height: 60px;
                            display: flex;
                            align-items: center;
                            position: relative;
                            cursor: pointer;
                            img{
                                width: 40px;
                                height: 40px;
                                margin:auto;
                                transition: all 0.2s;
                            }
                            .tooltip{
                                position: absolute;
                                top:0;
                                border-radius: 5px;
                                background-color: $blue-400;
                                transition: all 0.3s cubic-bezier(0.68, -0.55, 0.265, 1.55);
                                box-shadow: 0 10px 10px rgba(0, 0, 0, 0.1);
                                padding: 5px 8px;
                                color: $white;
                                opacity: 0;
                                pointer-events: none;
                                left: 50%;
                                transform: translate(-50%);
                                white-space: nowrap;
                                padding:0.5rem 0.8rem;
                            }
                            .tooltip::before {
                                position: absolute;
                                content: "";
                                height: 10px;
                                width: 10px;
                                background: $blue-400;
                                bottom: -3px;
                                left: 50%;
                                transform: translate(-50%) rotate(45deg);
                            }
                        }
                        .icon:hover img{
                            width: 50px;
                            height: 50px;
                            transform: scaleX(-1);
                        }
                        .icon:hover .tooltip{
                            opacity: 1;
                            top: -43px;
                            opacity: 1;
                            visibility: visible;
                        }
                    }
                    #icons:before, #icons:after{
                        content: "";
                        flex: 1 1;
                        border-bottom: 1px solid;
                        margin: auto;
                    }
                    #icons:before {
                    margin-right: 5px
                    }
                    #icons:after {
                    margin-left: 5px
                    }
                    
                    #technology{
                        height: 1.2em;
                        font-size: 1.2rem;
                        line-height: 1.2rem;
                        text-align: center;
                        color: white;
                        margin-bottom: 0.9rem;
                        margin-top: 0.4rem;
                    }
                }
                .buttons{
                    display: flex;
                    justify-content: space-between;
                }
            }
            
            #mockups-desktop{
                width: 36%;
                position: relative;
                display: flex;
                align-items: center;
                img{
                    width: 100%;
                }
            }
            
        }
    }
    @media screen and (max-width: 1700px) {
        #projects .content-container {
            #projects-desktop{
                width: 95%;
            }
            article{
                h1{
                    font-size: 3em;
                }
                .subtitle h2{
                    font-size: 1.5em;
                }
                p{
                    font-size: 1em;
                }

            }

        }
    }
    @media screen and (max-width: 1300px) {
        #projects .content-container #projects-desktop{
            article{
                h1{
                    font-size: 2.5em;
                }
                a{
                    padding: 0.7em 1.2em;
                }
            }
            #mockups-desktop{
            width: 38%;
            }
        }
    }
    @media screen and (max-width: 900px) {
        #projects .content-container {
            #projects-desktop{
                width: 100%;
            }
        }
    }
    @media screen and (max-width: 830px){
        #projects .content-container #projects-desktop{
            flex-direction: column-reverse;
            article{
                width: 80%;
                margin: auto;
                margin-bottom: 3em;
            }
            #mockups-desktop{
                margin: auto;
                margin-bottom: 2em;
            }
        }
    }
    @media screen and (max-width: 500px) {
        #projects .content-container #projects-desktop{
            display: none;
            width: 100%;
            
        }
        #projects-mobile{
            display: flex;
            flex-direction: column;
            width: 100%;

            img{
                width: 100vw;
            }
            .container{
                width: 80%;
                margin: auto;
                margin-top: -15px;
                h1{
                    font-size: 2em;
                    font-weight: 600;
                }
                .buttons{
                    margin: 1.5em 0;
                    a{
                        padding: 0.6rem 1.1rem;
                    }
                }
            }
        }
    }
</style>