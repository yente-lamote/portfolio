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
                        <div class="social-links">
                            <a class="link" aria-label="gitbhub profile" href="https://github.com/yente-lamote" target="_blank">
                                <img class="link-icon" src="@/assets/images/icons/github.png" alt="github icon"/>
                            </a>
                            <a class="link" aria-label="linkedin profile" href="https://www.linkedin.com/in/yente-lamote/" target="_blank">
                                <img class="link-icon" src="@/assets/images/icons/linkedin.png" alt="linkedIn icon"/>
                            </a>
                            <a class="link" aria-label="email" href="mailto: info@yentelamote.be" target="_blank">
                                <img class="link-icon" src="@/assets/images/icons/mail.png" alt="mail icon"/>
                            </a>
                        </div>
                    </div>
                </div>
                <div class="contact-side-container">
                    <form ref="form" id="contact-form" @submit.prevent="sendEmail">
                        <div id="name-container" class="input-container">
                            <label for="name" :class="{'label-focus': formInput.name.focus}">Name</label>
                            <input v-model="formInput.name.value" id="name" name="name" type="text" @focus="handleFocus('name')" @focusout="handleFocusout('name')" required>
                        </div>
                        <div id="email-container" class="input-container">
                            <label for="email" :class="{'label-focus': formInput.email.focus}">Email</label>
                            <input v-model="formInput.email.value" id="email" name="email" type="text" @focus="handleFocus('email')" @focusout="handleFocusout('email')" required>
                        </div>
                        <div id="message-container" class="input-container">
                            <label for="message" :class="{'label-focus': formInput.message.focus}">Message</label>
                            <textarea v-model="formInput.message.value" id="message" name="message" rows="6" @focus="handleFocus('message')" @focusout="handleFocusout('message')" required></textarea>
                        </div>
                        <div id="submit-container">
                            <input type="submit" value="Send message" :disabled="isDisabled">
                        </div>
                    </form>
                </div>
            </div>
            <FormSubmittedPopup v-if="showPopup" @showPopup="setShowPopup" :showError="showError"></FormSubmittedPopup>
    </section>
</template>
<script>
import emailjs from '@emailjs/browser';
import FormSubmittedPopup from '../components/FormSubmittedPopup.vue';

export default {
    data() {
        return {
            formInput: {
                name: {
                    focus: false,
                    value: ""
                },
                email: {
                    focus: false,
                    value: ""
                },
                message: {
                    focus: false,
                    value: ""
                },
            },
            isDisabled: false,
            showPopup:false,
            showError:false,
        };
    },
    methods: {
        setShowPopup(showPopup){
            this.showPopup=showPopup;
        },
        handleFocus(id) {
            this.formInput[id].focus = true;
        },
        handleFocusout(id) {
            if (!this.formInput[id].value) {
                this.formInput[id].focus = false;
            }
        },
        sendEmail() {
            this.isDisabled = true;
            emailjs.sendForm("service_9af7ekb", "template_c71ezr5", this.$refs.form, "q4vRdTEnLH-nwWNz4")
                .then((result) => {
                this.formInput.name.value = "";
                this.formInput.email.value = "";
                this.formInput.message.value = "";
                this.formInput.name.focus = false;
                this.formInput.email.focus = false;
                this.formInput.message.focus = false;
                this.isDisabled = false;
                this.showError=false
                this.showPopup=true;
            }, (error) => {
                this.isDisabled = false;
                this.showError=true;
                this.showPopup=true;
            });
        }
    },
    components: { FormSubmittedPopup }
}
</script>
<style lang="scss">
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
        input[type=submit]:disabled{
            opacity: 0.6 !important;
            background-color: $white !important;
            color:$blue-600 !important;
        }
        input[type=submit]{
            display: block;
            border:none;
            width: auto;
           
            background-color: $white;
            color:$blue-600;
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
            color:$white;
            background-color: $blue-500;
            cursor: pointer;
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
            margin: 1em 0;
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
            #links{
                font-size: 1.5em;
            }
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
            #links{
                font-size: 1em;
            }
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