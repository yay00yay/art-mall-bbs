<template>
  <div class="nav-top">
    <pc-nav class="pc-nav" />
    <tablet-nav class="tablet-nav" />
    <mobile-nav class="mobile-nav" />
  </div>
</template>

<script>
export default {}
</script>

<style lang="scss">
//顶部导航栏固定在顶部不动
.nav-top {
  position: fixed;
  top: 0px;
  left: 0px;
  right: 0px;
  z-index: 30;
}

// 当现实顶部导航栏的时候，顶部预留一段空白，防止重叠
body {
  @media screen and (min-width: 1024px) {
    padding-top: 110px;
  }

  @media screen and (min-width: 500px) and (max-width: 1024px) {
    padding-top: 46px;
  }

  @media screen and (max-width: 500px) {
    padding-top: 70px;
  }
}
</style>

<style scoped>
/* 屏幕宽度大于1024px时候显示pc nav */
@media screen and (min-width: 1024px) {
  .pc-nav {
    display: block !important;
  }
  .tablet-nav {
    display: none !important;
  }
  .mobile-nav {
    display: none !important;
  }
}

/* 屏幕宽度小于1024px，大于500px时候显示tablet nav */
@media screen and (min-width: 500px) and (max-width: 1024px) {
  .pc-nav {
    display: none !important;
  }
  .tablet-nav {
    display: block !important;
  }
  .mobile-nav {
    display: none !important;
  }
}

/* 屏幕宽度小于500px时候显示mobile nav, 上部导航栏 */
@media screen and (max-width: 500px) {
  .pc-nav {
    display: none !important;
  }
  .tablet-nav {
    display: none !important;
  }
  .mobile-nav {
    display: block !important;
  }
}
</style>
