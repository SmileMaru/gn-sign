<template>
    <header class="header">
        <img src="../assets/images/logo/logo-group.png" alt="" />
        <button class="record_btn">歷史記錄</button>
    </header>
</template>

<script>
    export default {
        
    }
</script>

<style lang="scss" scoped>
@import '../assets/scss/base/style.scss';
.header{
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    padding: 2rem 2rem;
    max-width: 85vw;
    @include margin_auto;
}
</style>