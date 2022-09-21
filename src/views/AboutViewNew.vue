<template lang="">
    <section id="about">
        <div id="about-container">
            <div id="profile-picture">
                <div>
                    <img src="@/assets/images/me.png" alt="photo of me"/>
                </div>
                <img id="hovered-photo" src="@/assets/images/me-hovered.png" alt="another photo of me"/>
            </div>
            <div id="about-content">
                <nav>
                    <ul>
                        <li>
                            <RouterLink to="/about">About me</RouterLink>
                        </li>
                        <li>
                            <RouterLink to="/about/experience">Experience</RouterLink>
                        </li>
                        <li>
                            <RouterLink to="/about/skills">Skills</RouterLink>
                        </li>
                    </ul>
                </nav>
                <div style="overflow:hidden; flex:1">
                    <div id="tabs" :style="{'transform':`translateX(-${translateX}px)`}">
                        <div id="about-me" class="tab">
                            <div>
                                <p>
                                    Hi, I'm Yente, a software developer based in Bruges. I'm specialized in both 
                                    back and font-end. I started programming in 2016. Since then I have already 
                                    gained some experience from internships and school projects. The projects I 
                                    enjoy working on are web applications and software with a lot of functionality.
                                </p>
                                <p>
                                    Besides software development I also have interests in artificial intelligence
                                    and tech in general.
                                </p>
                            </div>
                            <div id="links">
                                <a aria-label="gitbhub profile" href="https://github.com/yente-lamote">
                                    <img class="link-icon" src="@/assets/images/icons/iconmonstr-github-3.svg" alt="github icon"/>
                                </a>
                                <a aria-label="linkedin profile" href="https://www.linkedin.com/in/yente-lamote/">
                                    <img class="link-icon" src="@/assets/images/icons/iconmonstr-linkedin-3.svg" alt="linkedIn icon"/>
                                </a>
                                <a aria-label="email" href="#">
                                    <img class="link-icon" src="@/assets/images/icons/email.svg" alt="mail icon"/>
                                </a>
                            </div>
                        </div>
                        <div id="experience"  class="tab">
                            <div class="job">
                                <p class="title">Jobstudent IT - Dana</p>
                                <p class="period">July - September 2022</p>
                                <!-- <ul class="tasks">
                                    <li>Helped colleagues with hardware and software problems</li>
                                    <li>Developed in-house software applications</li>
                                    <li>Automated tasks with scripts</li>
                                </ul> -->
                            </div>
                            <div class="job">
                                <p class="title">Internship - D'M&S</p>
                                <p class="period">February - May 2021</p>
                                <!-- <ul class="tasks">
                                    <li>Backend developer in Drupal & Laravel</li>
                                    <li>Developed Lead Project</li>
                                    <li>Reasearch on when to use Laravel over Drupal and vice versa</li>
                                </ul> -->
                            </div>
                            <div class="job">
                                <p class="title">Internship - BMT Aerospace</p>
                                <p class="period">March 2018</p>
                                <!-- <ul class="tasks">
                                    <li>Helped colleagues with hardware and software problems</li>
                                </ul> -->
                            </div>
                        </div>
                        <div id="skills"  class="tab">
                            <p>
                                I'm specialized in both back and front-end but I must say that back-end is more of my expertise.
                                Below you can see couple of my skills.
                            </p>
                            <div id="skills-list">   
                                <span>HTML & CSS</span>
                                <span>JavaScript</span>
                                <span>PHP</span>
                                <span>Vue.js</span>
                                <span>Node.js</span>
                                <span>Laravel</span>
                                <span>Java</span>
                                <span>Python</span>
                                <span>C#</span>
                                <span>MySQL</span>
                                <span>GraphQL</span>
                                <span>Sass</span>
                                <span>Linux</span>
                                <span>ASP.NET</span>
                                <span>Git</span>
                                <span>PowerShell</span>
                                <span>Machine learning</span>
                                <span>Deep learning</span>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>
<script>
export default {
    data:()=>{
        return{
            tabs:[
                {
                    name:"about",

                    enter:()=>{},
                    leave:()=>{}
                },
                {
                    name:"experience",
                    enter:()=>{},
                    leave:()=>{}
                },
                {
                    name:"skills",
                    enter:()=>{},
                    leave:()=>{}
                },
            ],
            translateX:0,
            tabWidth:0,
            currentTab:0
        }
    },
    watch:{
        $route (to, from){
            let newTab = this.tabs.filter(function(el){return el.name == to.name})[0]
            let prevTab = this.tabs.filter(function(el){return el.name == from.name})[0]
            if(newTab){
                this.currentTab=this.tabs.indexOf(newTab)           
            }
      }
    },
    computed:{
        translateX(){
        return this.tabWidth*this.currentTab
      }
    },
    methods:{
        async calculateTabWidth(){
          this.tabWidth = document.querySelector("#about-me").offsetWidth
          await new Promise(resolve => setTimeout(resolve, 1050));
          this.tabWidth = document.querySelector("#about-me").offsetWidth
          console.log(this.tabWidth)
          // Then we set the value in the --vh custom property to the root of the document
          document.documentElement.style.setProperty('--tabWidth', `${this.tabWidth}px`)
      },
      forceUpdate(){
        this.$forceUpdate();
      }
    },
    mounted(){
      this.calculateTabWidth();
      window.addEventListener("resize",this.calculateTabWidth)
    }
}
</script>
<style lang="scss">
    .tagcloud--item{
        font-size: 0.7em;
    }
    #skills{
        position: relative;
    }
    #tagcloud{
        position: absolute;
        top: 50%;
        transform: translateY(-50%);
        
    }
    #about{
        position: relative;
        #about-container{
            position: absolute;
            top:50%;
            left: 50%;
            transform: translate(-50%,-50%);
            width:70%;
            display: flex;
        
            #profile-picture{
                position: relative;
                width: 35%;
                height: 0;
                padding-bottom: 35%;
                img{
                    position: absolute;
                    height: 100%;
                    width: 100%;
                }
                #hovered-photo{
                    visibility: hidden;
                }
                div::after{
                    content:"";
                    position: absolute;
                    background-color: $blue-200;
                    width: 100%;
                    height: 100%;
                    opacity: 0.5;
                }
            }
            #profile-picture::before{
                content:"";
                position: absolute;
                background-color: #001720;
                width: 100%;
                height: 100%;
                margin-top: 10px;
                margin-left: 10px;
            }
            #profile-picture:hover #hovered-photo{
                visibility: visible;
            }

            #about-content{
                ul{
                    position: relative;
                    li{
                        display: inline-block;
                        a{
                            text-decoration: none;
                            padding:0.1rem 0;
                            font-weight: 600;
                            font-size: 1.2rem;
                            color:$grey;
                        }
                        margin-right: 3rem;
                        .router-link-exact-active{
                            color: $white;
                        }
                    }
                    margin-bottom: 1rem;
                }
                ul::before{
                    content:"";
                    height: 1.05px;
                    background-color: $pink;
                    width: 24%;
                    position: absolute;
                    left: -28%;
                    top:50%;
                }
            }

            //right side
            #about-content{
                margin-left: 5%;
                margin-top:2%;
                width: 50%;
                display: flex;
                flex-direction: column;
                
                #tabs{
                    height: 100%;
                    display: flex;
                    width: 300%;
                    transition: all 1000ms cubic-bezier(0.645, 0.045, 0.355, 1) 0s;
                    transition-property: all;
                    transition-duration: 1000ms;
                    transition-timing-function: cubic-bezier(0.645, 0.045, 0.355, 1);
                    transition-delay: 0s;
                }
                .tab{
                    width: 100%;
                    height: 100%;
                }
                p{
                    line-height: 1.5;
                    margin-bottom:1em;
                    color:$grey;        
                }
                #about-me{
                    display: flex;
                    flex-direction: column;
                    justify-content: space-between;
                    #links{
                        display: inline-block;
                        a{
                            margin-right: 10px;
                            .link-icon{
                                width: 30px;
                                height: 30px;
                            }
                        }
                    }
                }

                #experience{
                    margin-top:1em;
                    .job:first-of-type{
                        border-top: 1px solid $white;
                    }
                    .job{
                        border-bottom: 1px solid $white;
                        padding: 0.7em;
                        .title{
                            color: $white;
                            font-size: 1.2em;
                            margin-top: 0;
                            margin-bottom: 0;
                        }
                        .period{
                            margin-bottom: 0.2em;
                        }
                    }
                }
                #skills{
                    display: flex;
                    justify-content: space-between;
                    flex-direction: column;
                }
                #skills-list{
                    span{
                        display: inline-block;
                        padding: 0.5em 1em;
                        margin: 0.2em;
                        border: 1px solid $white;
                    }
                }
            }
        }
    }
</style>