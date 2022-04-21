<template>
  <div class="nav-bottom">
    <!-- T: 04200328 -->
    <!-- 移动端分上下两部分导航栏 -->
    <mobile-subdown-nav class="mobile-subdown-nav" />
  </div>
</template>

<script>
export default {}
</script>

<style scoped>
/* 底部导航栏固定在底部不不动 */
.nav-bottom {
  position: fixed;
  bottom: 0px;
  left: 0px;
  right: 0px;
  z-index: 30px;
}
/* 底部导航栏只在屏幕宽度小于500px时候显示出来 */
@media screen and (min-width: 500px) {
  .mobile-subdown-nav {
    display: none !important;
  }
}
@media screen and (max-width: 500px) {
  .mobile-subdown-nav {
    display: block !important;
  }
}
</style>
