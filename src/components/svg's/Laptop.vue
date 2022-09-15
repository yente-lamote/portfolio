<template lang="">
    <div>
        <div>
            <img id="lid" src="@/assets/images/lid.png" alt="laptop lid with lead-project on screen"/>
            <img id="bottom" src="@/assets/images/bottom.png" alt="laptop keyboard"/>
        </div>
    </div>
</template>
<script>
export default {
    
}
</script>
<style lang="scss">
    #lid{
        width: 105%;
        margin-left: auto;
        margin-right: auto;
        transform-origin:65% 100%;
    }
    #bottom{
        position: absolute;
        width: 100%;
        left: 0;
        bottom: 0;
    }
    
    #screen{
        background: #0c0303;
    }
    .cls-1 {
      fill: #7f7878;
    }

    .cls-2 {
      fill: #fff;
    }

    .cls-3 {
      fill: #b7b6b6;
    }

    .cls-4 {
      fill: #f4eaea;
    }

    .cls-5 {
      fill: #0c0303;
    }
  </style>