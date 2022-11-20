<template>
  <div class="loading_animate" ref="container">
      <div class="loading_text_box">
          <p class="loading_text">上傳中......</p>
      </div>
  </div>
</template>

<script>
import lottie from "lottie-web"
import jsonData from "@/assets/json/pencil_animated.json"

export default {
    //參考網路上的教學，原理還不清楚
      data(){
          return{
              anim: null
          }
      },
      mounted(){
          this.anim = lottie.loadAnimation({
              container: this.$refs.container,
              renderer: 'svg',
              loop: true,
              autoplay: true,
              animationData: jsonData,
          })
      }
  }
</script>

<style lang="scss" scoped>
    svg{
        width: 100px;
    }
</style>