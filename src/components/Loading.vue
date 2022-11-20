<template>
    <div class="loading_animate" ref="container">
        <div class="loading_text_box">
            <p class="loading_text">簽名優化中......</p>
        </div>
    </div>
</template>

<script>
import lottie from "lottie-web"
import jsonData from "@/assets/json/loading_pencil.json"

export default {
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

</style>