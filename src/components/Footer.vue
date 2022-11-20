<template>
    <footer class="footer">
        <p class="copy_right">小綠簽 © Code: Maru  /  Design: KT</p>
    </footer>
</template>

<script>
    export default {
        
    }
</script>

<style lang="scss" scoped>
@import "../assets/scss/base/style.scss";
.copy_right{
    position: absolute;
    right: 3vw;
    bottom: 0.5vw;
    font-weight: 400;
    font-size: 12px;
    @include sm(){
        left: 25%;
    }
}

</style>