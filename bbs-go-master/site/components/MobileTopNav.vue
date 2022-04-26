<template>
  <div class="navbar">
    <mobile-top-nav-header></mobile-top-nav-header>
    <mobile-top-nav-tabs></mobile-top-nav-tabs>
  </div>
</template>

<script>
import UserHelper from '~/common/UserHelper'

export default {
  data() {
    return {
    }
  },
  computed: {
    user() {
      return this.$store.state.user.current
    },
    isOwnerOrAdmin() {
      return UserHelper.isOwner(this.user) || UserHelper.isAdmin(this.user)
    },
    config() {
      return this.$store.state.config.config
    }
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

<style lang="scss" scoped>
.navbar {
  /*opacity: 0.99;*/
  /*border-bottom: 1px solid #e7edf3;*/
  background-color: var(--bg-color);
  position: fixed;
  top: 0px;
  left: 0px;
  right: 0px;
  z-index: 30;
}
</style>
