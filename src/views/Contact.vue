<template>
    <section>
        <div id="contact-container">
            <div>
                <div id="contact">
                    <h1>
                    Contact
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
            <div>
                <p>form placeholder</p>
            </div>
        </div>
    </section>
</template>
<script>
export default {
    
}
</script>
<style lang="scss">
    #contact-container{
        display: flex;
        color:$white;
        top:50%;
        position: absolute;
        transform:translateY(-50%);
        div{
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
            width:70%;
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