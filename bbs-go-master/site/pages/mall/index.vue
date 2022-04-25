<template>
  <section class="main">
    <van-swipe class="my-swipe" :autoplay="3000" indicator-color="white">
        <van-swipe-item>1</van-swipe-item>
        <van-swipe-item>2</van-swipe-item>
        <van-swipe-item>3</van-swipe-item>
        <van-swipe-item>4</van-swipe-item>
    </van-swipe>
  </section>
</template>

<script>
export default {}
</script>

<style lang="scss" scoped>
.my-swipe {
    height: 300px;
    background-color: gray;
}
</style>
