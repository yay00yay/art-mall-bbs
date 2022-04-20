<template>
  <div>
    <pc-nav class="pc-nav" />
    <mobile-nav class="mobile-nav" />
    <!-- T: 04200328 -->
    <!-- 移动端分上下两部分导航栏 -->
    <mobile-subup-nav class="mobile-subup-nav" />
  </div>
</template>

<script>
export default {}
</script>

<style lang="scss">
// 当现实顶部导航栏的时候，顶部预留一段空白，防止重叠
body {
  @media screen and (max-width: 1024px) {
    padding-top: 46px;
  }
}
</style>

<style scoped>
@media screen and (min-width: 1024px) {
  .pc-nav {
    display: block !important;
  }
  .mobile-nav {
    display: none !important;
  }
  .mobile-subup-nav {
    display: none !important;
  }
}

/* T: 04200328 */
@media screen and (min-width: 500px) and (max-width: 1024px) {
  .pc-nav {
    display: none !important;
  }
  .mobile-nav {
    display: block !important;
  }
  .mobile-subup-nav {
    display: none !important;
  }
}

@media screen and (max-width: 500px) {
  .pc-nav {
    display: none !important;
  }
  .mobile-nav {
    display: none !important;
  }
  .mobile-subup-nav {
    display: block !important;
  }
}
</style>
