<template lang="">
    <section id="about">
        <div class="absolute-vertical-centered">
            <div id="about-grid">
                <div class="grid-item left top">
                    <p><span>22</span><br>Years Old</p>
                    <h1>About Me</h1>
                </div>
                <div class="grid-item right top">
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
                <div class="grid-item left bottom">
                    <div id="profile-picture">
                        <div>
                            <img src="@/assets/images/me.png" alt="photo of me"/>
                        </div>
                        <img id="hovered-photo" src="@/assets/images/me-hovered.png" alt="another photo of me"/>
                        
                    </div>
                </div>
                <div class="grid-item right bottom">
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
            </div>
        </div>
    </section>
</template>
<script>
export default {
    
}
</script>
<style lang="scss">
    #about{
        position: relative;
        #about-grid{
            width: 80%;
            height: 80vh;
            display: grid;
            position: absolute;
            top:50%;
            left:50%;
            transform: translate(-50%, -50%);
            grid-template-columns: 50% 50%;
            grid-template-rows: 50% 50%;
        }
        .grid-item{
            position: relative;
            padding:5% 10%;
        }
        .left{
            padding-right: 20%;
        }
        .right{
            padding-left: 20%;
        }
        //left top
        .left.top{
            h1{
                font-size: 2em;
                position: absolute;
                transform: translate(-50%, -50%);
                top:50%;
                left:50%;
                font-weight: 600;
            }
            p{
                font-size:1.4em;
                span{
                    font-size:1.4em;
                    font-weight: bold;
                }
            }
        }
        .left::after, .right::after, .bottom::before, .top::before{
            background-color: $grey;
            position: absolute;
            content: "";
        }
        .left::after, .right::after{
            width: 0.5px;
            height: 45%;
        }
        .bottom::before, .top::before{
            width: 45%;
            height: 0.5px;
        }
        .bottom .top{
            height: 0.5px;
        }
        //vertical lines
        .left.top::after{
            right: 0;
            top:20%;       
        }
        .right.top::after{
            left: 0;
            top:20%;       
        }
        .left.bottom::after{
            right: 0;
            bottom:20%;       
        }
        .right.bottom::after{
            left: 0;
            bottom:20%;       
        }
        //horizontal lines
        .left.top::before, .right.top::before{
            left: 50%;
            transform: translateX(-50%);
            bottom: 0;       
        }
        .left.bottom::before, .right.bottom::before{
            left: 50%;
            transform: translateX(-50%);
            top: 0;    
        }

        //right top
       .right.bottom{
            .job:first-of-type{
                padding-top: 0;
            }
            .job:last-of-type{
                border: none;
            }
            .job{
                padding-bottom: 0.7em;
                padding-top: 0.7em;
                border-bottom: 1px solid $grey;
                padding-left: 8px;
                .title{
                    font-size: 1.3em;
                }
                .period{
                    font-size: 1em;
                    color: $grey;
                }
                .tasks{
                    margin-top: 7px;
                    li{
                        font-size: 0.8em;
                        margin-top: 8px;
                        position: relative;
                        margin-left: 5px;
                        padding-left: 16px;
                    }
                    li::before{
                        content: "";
                        position: absolute;
                        width: 8px;
                        height: 8px;
                        background-color: $pink;
                        border-radius: 50%;
                        top: 50%;
                        transform: translateY(-50%);
                        left: 0;
                    }
                }
            }
        }
        //left bottom
        #profile-picture{
            position: relative;
            width: 80%;
            height: 0;
            padding-bottom: 80%;
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
                opacity: 0.32;
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
    }
</style>