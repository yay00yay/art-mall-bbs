<template>
  <div>
    <!-- T:04200953 -->
    <div v-if="activeDomain === 'mall'" class="navbar-submenu" :class="{'is-hidden': hideSubMenu}">
      <van-tabs v-model="activeName" @click="onClickSubMenu" class="navbar-submenu-tabs">
        <van-tab title="首页" name="home"></van-tab>
        <van-tab title="最新" name="newest"></van-tab>
        <van-tab title="推荐" name="recommend"></van-tab>
      </van-tabs>
    </div>
    <div v-if="activeDomain === 'community'" class="navbar-submenu">
      <van-tabs v-model="activeName" @click="onClickSubMenu" class="navbar-submenu-tabs">
        <van-tab title="首页" name="home"></van-tab>
        <van-tab title="话题" name="topics"></van-tab>
        <van-tab title="文章" name="articles"></van-tab>
      </van-tabs>
    </div>
    <div v-if="activeDomain === 'meta'" class="navbar-submenu">
      <van-tabs v-model="activeName" @click="onClickSubMenu" class="navbar-submenu-tabs">
        <van-tab title="星艺术" name="arts"></van-tab>
        <van-tab title="星空间" name="spaces"></van-tab>
        <van-tab title="星人惹" name="artiests"></van-tab>
      </van-tabs>
    </div>
  </div>
</template>

<script>
import UserHelper from '~/common/UserHelper'
// T:04200953
const defaultDomain = 'community' // 1. community 2. mall 3. artwork

export default {
  data() {
    return {
      hideSubMenu: false
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
    },
    // T:04200953
    activeDomain() {
      if (this.$route.path.includes('mall')) {
        return 'mall'
      } else if (this.$route.path.includes('meta')) {
        return 'meta'
      } else if (this.$route.path.includes('community')) {
        return 'community'
      } else {
        return defaultDomain
      }
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
    onClickSubMenu(name, title) {
      const firstRoute = this.activeDomain === 'community' ? "" : '/' + this.activeDomain
      const secondRoute = name === 'home' ? "" : "/" + name
      const toPath = firstRoute + secondRoute;
      this.$linkTo(toPath)
    },
  },
}
</script>

<style lang="scss" scoped>
  .navbar-submenu {
    display: flex;
    padding: 0.5rem 0.75rem;
    justify-content: space-evenly;
  }

  .navbar-submenu-tabs {
    width: -webkit-fill-available;
  }

  .hidden {
    display: none;
  }
</style>
