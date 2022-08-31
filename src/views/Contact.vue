<template>
    <section>
        <div id="contact-container">
            <div class="w-50">
                <div id="contact">
                    <h1>
                        Get in touch
                    </h1>
                    <p>
                        I'm interested in freelance and job opportunities. However, if you have any other 
                        request or question, don't hesitate to send me a 
                        message.
                    </p>
                    <a href="https://github.com/yente-lamote">
                        yente-lamote
                    </a>
                    <a href="https://www.linkedin.com/in/yente-lamote/">
                        yente-lamote
                    </a>
                    <a href="#">
                        info@yentelamote.be
                    </a>
                </div>
            </div>
            <div class="w-50">
                <form id="form">
                    <div class="input-container">
                        <div class="background"></div>
                        <label>Name</label>
                        <input type="text">
                    </div>
                    <div class="input-container">
                        <div class="background"></div>
                        <label>Email</label>
                        <input type="text">
                    </div>
                    <div class="input-container">
                        <div class="background"></div>
                        <label>Subject</label>
                        <input type="text">
                    </div>
                    <div class="input-container">
                        <div class="background"></div>
                        <label>Message</label>
                        <textarea id="message" rows="6"></textarea>
                    </div>
                    <input type="submit" value="Submit">
                </form>
            </div>
        </div>
    </section>
</template>
<script>
export default {
    
}
</script>
<style lang="scss">
    #form{
        width: 75%;
        margin: auto;
        .input-container{
            position: relative;
            margin-bottom: 0.8em;
            border-radius: 4px;
        }
        .background{
            position: absolute;
            height: 100%;
            width: 100%;
            background-color: $white;
            z-index: -20;
        }
        label{
            display: block;
            font-size: 1rem;
            margin-bottom: 0.3em;
            color: #000;
            transform: translateY(43%) translateX(3.2%);
            position: absolute;
            z-index: -1;
            width: 100%;
            height: 20px;
        }
        input,textarea{
            padding: 0.6em 0.8em;
            text-decoration: none;
            font-size:1rem;
            border: none;
            box-sizing: border-box;
            outline: none;
            width:100%;
            background-color: transparent;
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
        }
    }
    #contact-container{
        display: flex;
        color:$white;
        width: 70%;
        top:50%;
        position: absolute;
        transform:translateY(-50%);
        .w-50{
            width: 50%;
            h1{
                font-size: 3em;
            }
            p{
                color:$grey;
                font-size: 1.3rem;
            }
        }
        #contact{
            height: 80%;
            margin-left:1em;
            p{
                margin-bottom: 10rem;
            }
            a{
                display: block;
            }
        }
    }

</style>