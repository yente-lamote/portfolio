<template>
    <section id="contact">
        <div class="content-container">
                <div id="left-contact-side-container" class="contact-side-container">
                    <div id="contact-info">
                        <div>
                            <h1>
                                Get in touch
                            </h1>
                            <p>
                                I'm interested in freelance projects and job opportunities. However, if you have any other 
                                request or question, don't hesitate to send me a 
                                message.
                            </p>
                        </div>
                        <div id="arrow">
                        </div>
                        <div id="links">
                            <a aria-label="gitbhub profile" href="https://github.com/yente-lamote">
                                <img class="link-icon" src="@/assets/images/icons/iconmonstr-github-3.svg" alt="github icon"/>
                            <span class="handle">yente-lamote</span>
                            </a>
                            <a aria-label="linkedin profile" href="https://www.linkedin.com/in/yente-lamote/">
                                <img class="link-icon" src="@/assets/images/icons/iconmonstr-linkedin-3.svg" alt="linkedIn icon"/>
                                <span class="handle">yente-lamote</span>
                            </a>
                            <a aria-label="email" href="#">
                                <img class="link-icon" src="@/assets/images/icons/email.svg" alt="mail icon"/>
                                <span class="handle">info@yentelamote.be</span>
                            </a>
                        </div>
                    </div>
                </div>
                <div class="contact-side-container">
                    <form id="contact-form">
                        <div class="input-container">
                            <label for="name" :class="{'label-focus': formInput.name.focus}">Name</label>
                            <input v-model="formInput.name.value" id="name" type="text" @focus="handleFocus('name')" @focusout="handleFocusout('name')">
                        </div>
                        <div class="input-container">
                            <label for="email" :class="{'label-focus': formInput.email.focus}">Email</label>
                            <input v-model="formInput.email.value" id="email" type="text" @focus="handleFocus('email')" @focusout="handleFocusout('email')">
                        </div>
                        <div class="input-container">
                            <label for="message" :class="{'label-focus': formInput.message.focus}">Message</label>
                            <textarea v-model="formInput.message.value" id="message" rows="6" @focus="handleFocus('message')" @focusout="handleFocusout('message')"></textarea>
                        </div>
                        <input type="submit" value="Send message">
                    </form>
                </div>
            </div>
    </section>
</template>
<script>
export default {
    data(){
        return{
            formInput:{
                name:{
                    focus:false,
                    value:""
                },
                email:{
                    focus:false,
                    value:""
                },
                message:{
                    focus:false,
                    value:""
                },
            }
        }
    },
    methods:{
        handleFocus(id){
            this.formInput[id].focus=true
        },
        handleFocusout(id){
            console.log(this.formInput[id])
            if(!this.formInput[id].value){
                this.formInput[id].focus=false
            }
        }
    }
}
</script>
<style lang="scss">
    #links{
        a{
            display: flex;
            justify-content: center;
        }
    }
    .link-icon{
        width: 20px;
        height: 20px;
    }
    #contact-form{
        width: 75%;
        margin: auto;
        padding-top: 1.8em;
        .input-container{
            position: relative;
            margin-bottom: 1.9em;
        }
 
        label{
            display: block;
            font-size: 1rem;
            color:$white;
            padding: 0.4em 0;
            transform: translateY(-5%);
            position: absolute;
            z-index: -1;
            width: 100%;
            -webkit-transition: all 0.15s linear;
            -moz-transition: all 0.15s linear;
            -o-transition: all 0.15s linear;
            transition: all 0.15s linear;
            border-radius: 3px;
            color: $grey;
        }
        .label-focus{
            transform: translateY(-80%);
            color: $white;
        }
        input,textarea{
            padding: 0.4em 0.1em;
            font-size:1rem;
            color: $grey;
            border: none;
            outline: none;
            width:100%;
            background-color: transparent;
            max-width: 100%;
            border-width: 0 0 1px 0;
            border-color: $grey;
            border-style: solid;
        }
        input:-webkit-autofill,
        input:-webkit-autofill:hover,
        input:-webkit-autofill:focus,
        input:-webkit-autofill:active {
            transition: background-color 5000s ease-in-out 0s;
            -webkit-text-fill-color: white !important;
        }
        #message{
            width:100%;
        }
        #name-email-container{
            display: flex;
            justify-content: space-between;
            div{
                display: flex;
                flex-direction: column;
                width: 48%;
            }
        }
        input[type=submit]{
            display: block;
            border:none;
            width: auto;
            color:$blue-400;
            background-color: $white;
            margin-left: auto;
            padding:0.8em 1.5em;
            font-weight: 600;
            border-radius: 10px;
            -webkit-transition: all 0.15s linear;
            -moz-transition: all 0.15s linear;
            -o-transition: all 0.15s linear;
            transition: all 0.15s linear;
        }
        input[type=submit]:hover{
            background-color: $pink;
            color:$white;
        }
    }

    #contact .content-container{
        color:$white;
        width: 70%;
        left:50%;
        transform:translateY(-50%) translateX(-50%);
        h1{
            font-size: 3em;
            margin-bottom: 0.3em;
        }
        .contact-side-container{
            width: 50%;
            position:relative;
            p{
                width: 80%;
                color:$grey;
                font-size: 1.2rem;
            }
        }
        #contact-info{
            height: 100%;
            display: flex;
            flex-direction: column;
            a{
                color:$grey;
                padding: 0.2em 0;
                span{
                    margin-right: auto;
                    margin-left: 5px;
                }
            }
            
        }
        #arrow{
            flex-grow: 1;
            border-left: 1px;
            border-color: $pink;
            border-style: solid;
            margin: .5em 0;
        }
    }
    @media screen and (max-width: 950px) {
        #contact .content-container{
            flex-direction: column;
            left:47%;
            h1{
                font-size:3.2em;
            }
            .contact-side-container{
                width:100%;
                p{
                    width: 100%;
                    font-size: 1.5em;
                }
            }
        }
        #links{
            font-size: 1.5em;
        }
        #contact-form{
            width: 100%;
            margin-top:1.4em;
        }
    }
    @media screen and (max-width: 500px) {

        #contact .content-container{
            h1{
            font-size:2em;
            }
            .contact-side-container{
                p{
                    font-size: 1.2em;
                }
            }
        }
        #links{
            font-size: 1em;
        }

        textarea{
            height: 5em;
        }
        #contact-form{
            margin-top:0.5em;
            padding-top: 1em;
            display: none;
            width: 72%;
            input, textarea{
                font-size: 1em;
            }
            
        }
    }


</style>