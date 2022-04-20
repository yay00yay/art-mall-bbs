<template>
  <div class="mobile-tabbar">
    <div class="tabbar-menus">
      <div class="tabbar-menu-item">
        <nuxt-link :to="'/user/' + user.id">个人中心</nuxt-link>
      </div>
      <div class="tabbar-menu-item">
        <nuxt-link class="tabbar-menu-item" to="/user/favorites"
          >我的收藏</nuxt-link
        >
      </div>
      <div class="tabbar-menu-item">
        <nuxt-link class="tabbar-menu-item" to="/user/profile"
          >编辑资料</nuxt-link
        >
      </div>
    </div>
  </div>
</template>

<script>
import UserHelper from '~/common/UserHelper'
export default {
  computed: {
    show() {
      return this.$store.state.env.showMobileSidebar
    },
    user() {
      return this.$store.state.user.current
    },
    isOwnerOrAdmin() {
      return UserHelper.isOwner(this.user) || UserHelper.isAdmin(this.user)
    },
    config() {
      return this.$store.state.config.config
    },
    siteNavs() {
      const config = this.$store.state.config.config
      return config.siteNavs || []
    },
  },
  methods: {
    async signout() {
      try {
        await this.$store.dispatch('user/signout')
        this.$linkTo('/')
      } catch (e) {
        console.error(e)
      }
    },
  },
}
</script>
<style lang="scss" scoped></style>
