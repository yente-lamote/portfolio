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
                                    gained some experience from internships and school projects. <span class="side-information">The projects I 
                                    enjoy working on are web applications and software with a lot of functionality.</span>
                                </p>
                                <p class="side-information">
                                    Besides software development I also have interests in artificial intelligence
                                    and tech in general.
                                </p>
                            </div>
                            <div id="links" class="side-information">
                                <a aria-label="gitbhub profile" href="https://github.com/yente-lamote">
                                    <img class="link-icon" src="@/assets/images/icons/iconmonstr-github-3.svg" alt="github icon"/>
                                </a>
                                <a aria-label="linkedin profile" href="https://www.linkedin.com/in/yente-lamote/">
                                    <img class="link-icon" src="@/assets/images/icons/iconmonstr-linkedin-3.svg" alt="linkedIn icon"/>
                                </a>
                                <a aria-label="email" href="mailto: info@yentelamote.be">
                                    <img class="link-icon" src="@/assets/images/icons/email.svg" alt="mail icon"/>
                                </a>
                            </div>
                        </div>
                        <div id="experience"  class="tab">
                            <div id="jobs">
                                <div class="job">
                                    <div>
                                        <p class="company">Dana</p>
                                        <p class="title">Jobstudent - IT</p>
                                    </div>
                                    <div>
                                        <p class="period">3 Months</p>
                                        <p class="year">2022</p>
                                    </div>
                                    
                                    <!-- <ul class="tasks">
                                        <li>Helped colleagues with hardware and software problems</li>
                                        <li>Developed in-house software applications</li>
                                        <li>Automated tasks with scripts</li>
                                    </ul> -->
                                </div>
                                <div class="job">
                                    <div>
                                        <p class="company">D'M&S</p>
                                        <p class="title">Internship - Backend developer</p>
                                    </div>
                                    <div>
                                        <p class="period">4 Months</p>
                                        <p class="year">2021</p>
                                    </div>
                                    <!-- <ul class="tasks">
                                        <li>Backend developer in Drupal & Laravel</li>
                                        <li>Developed Lead Project</li>
                                        <li>Reasearch on when to use Laravel over Drupal and vice versa</li>
                                    </ul> -->
                                </div>
                                <div class="job">
                                    <div>
                                        <p class="company">BMT Aerospace</p>
                                        <p class="title">Internship - IT</p>
                                    </div>
                                    <div>
                                        <p class="period">1 Month</p>
                                        <p class="year">2018</p>
                                    </div>                                <!-- <ul class="tasks">
                                        <li>Helped colleagues with hardware and software problems</li>
                                    </ul> -->
                                </div>
                            </div>
                        </div>
                        <div id="skills"  class="tab">
                            <p>
                                I'm specialized in both back and front-end but I must say that back-end is more of my expertise.
                                <span class="side-information">Below you can see some of my skills.</span>
                            </p>
                            <div id="skills-list">   
                                <span>HTML & CSS</span>
                                <span>JavaScript</span>
                                <span>PHP</span>
                                <span>Vue.js</span>
                                <span>Node.js</span>
                                <span>Laravel</span>
                                <span>Java</span>
                                <span class="less-important">Python</span>
                                <span class="less-important">C#</span>
                                <span>MySQL</span>
                                <span class="less-important">GraphQL</span>
                                <span class="less-important">Sass</span>
                                <span>Linux</span>
                                <span class="less-important">ASP.NET</span>
                                <span class="less-important">Git</span>
                                <span class="less-important">PowerShell</span>
                                <span class="less-important">Machine learning</span>
                                <span class="less-important">Deep learning</span>
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
    data(){
      return{
            tabs:[
                {
                    name:"about",

                    enter:()=>{},
                    leave:()=>{}
                },
                {
                    name:"experience",
                    enter:this.experienceEnter,
                    leave:this.experienceLeave
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
            if(prevTab!=undefined){
                prevTab.leave()
            }
            if(newTab!=undefined){
                this.currentTab=this.tabs.indexOf(newTab)
                newTab.enter()
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
          // Then we set the value in the --vh custom property to the root of the document
          document.documentElement.style.setProperty('--tabWidth', `${this.tabWidth}px`)
        },
        experienceEnter(){
            const tl = gsap.timeline({defaults:{duration:0.9,ease: Power1.easeIn},onComplete:this.animationComplete})
            tl.fromTo("#jobs",{"width":"50%"},{"width":"100%"})
        },
        experienceLeave(){
            const tl = gsap.timeline({defaults:{duration:0.6,ease: Power1.easeIn},onComplete:this.animationComplete})
            tl.fromTo("#jobs",{"width":"100%"},{"width":"50%"})
        }
      
    },
    mounted(){
      this.calculateTabWidth();
      window.addEventListener("resize",this.calculateTabWidth)
    }
}
</script>
<style lang="scss">
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
                    opacity: 0.4;
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
                            font-size: 1.4rem;
                            color:$grey;
                        }
                        margin-right: 3rem;
                        .router-link-exact-active{
                            color: $white;
                            border-bottom: 2px solid $pink;
                        }
                    }
                    margin-bottom: 1.8rem;
                }
                /*ul::before{
                    content:"";
                    height: 1.05px;
                    background-color: $pink;
                    width: 24%;
                    position: absolute;
                    left: -28%;
                    top:50%;
                }*/
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
                    #jobs{
                        margin: auto;
                    }
                    /*
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
                    }*/
                    .job:last-of-type{
                        border:none;
                    }
                    .job:first-of-type{
                        padding-top: 0.8em;
                    }
                    .job{
                        margin: auto;
                        display: flex;
                        justify-content: space-between;
                        align-items:flex-end;
                        padding: 1.1em 0.8em;
                        border-bottom: 1px solid $white;
                        overflow: hidden;
                        p, span{
                            overflow:hidden;
                            white-space: nowrap;
                        }
                        .company{
                            font-size: 1.2em;
                            font-weight: 600;
                            color: $white;
                            margin-bottom:0;
                        }
                        .title{
                            margin:0;
                            font-size: 1em;
                            
                        }
                        .period{
                            color:$grey;
                            margin:0;
                            font-size: 0.9em;
                            line-height: 1em;
                        }
                        .year{
                            color: $white;
                            text-align: right;
                            line-height: 1.4;
                            font-size: 1em;
                            font-weight: 600;
                            margin:0;
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
                        margin: 0.5em;
                        border: 1px solid $white;
                    }
                }
            }
        }
    }
    @media screen and (max-width: 1650px) {
        #about #about-container{
            width: 75%;
        }
        #about #about-container #about-content #skills-list span{
            margin:0.35em;
            padding: 0.5em 1em;
        }
    }
    @media screen and (max-width: 1300px) {
        #about #about-container{
            width: 90%;
        }
    }
    @media screen and (max-width: 1200px) {
        #about #about-container{
            width: 100%;
            #about-content{
                width: 55%;
            }
        }
        
    }
    @media screen and (max-width: 1000px) {
        #about #about-container{
            #about-content{
                width: 60%;
            }
        }
        #about #about-container #about-content #experience{
            .job:first-of-type{
                padding-top: 0;
            }
            .job{
                padding:0.8em;
                .company{
                font-size: 1.2em;
                }
            }
            
        }
        #about #about-container #about-content #skills-list .less-important{
            display: none;
        }
    }
    @media screen and (max-width: 1000px) and (min-width:800px){
        #about #about-container {
            #about-content{
            flex-direction: row;
            width: 90%;
                nav{
                    width: 30%;
                }
                nav ul {
                    display: flex;
                    flex-direction: column;
                    justify-content: space-between;
                    position: absolute;
                    top: 50%;
                    transform: translateY(-50%);
                    li{
                        margin: 1em;
                    }
                }
            }
            #profile-picture{
                display: none;
            }
        }
        #about #about-container #about-content #skills-list .less-important{
            display: inline-block;
        }
    }
    @media screen and (max-width: 800px) {
        #about #about-container {
            width: 80%;
            flex-direction: column;
            #about-content{
                width: 90%;
            }
            #profile-picture{
                width: 70%;
                padding-bottom: 70%;
                margin: auto;
                margin-bottom: 1em;
            }
            
        }
        #about #about-container #about-content #skills-list .less-important{
            display: none;
        }
        #about #about-container #about-content #experience .job{
            .company{
                font-size: 1em;
            }
            .title{
                font-size: 0.9em;
            }
            .period{
                display: none;
            }
            .year{
                display: none;
            }
        } 
        #about #about-container #about-content ul{
            display: flex;
            justify-content: space-between;
            margin-top:0.5rem;
            margin-bottom: 1.5rem;
            li{
                margin-right: 0;
            }
        }
        .side-information{
            display: none !important;
        }
        #about #about-container #about-content #skills-list span{
            margin:0.3em;
            padding: 0.5em;
            font-size: 0.8em;
        }
    }
</style>