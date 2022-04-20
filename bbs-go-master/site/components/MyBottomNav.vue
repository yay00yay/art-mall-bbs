<template>
  <div>
    <!-- T: 04200328 -->
    <!-- 移动端分上下两部分导航栏 -->
    <mobile-subdown-nav class="mobile-subdown-nav" />
  </div>
</template>

<script>
export default {}
</script>

<style scoped>
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
