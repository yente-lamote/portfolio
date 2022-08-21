<template lang="">
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
</style>