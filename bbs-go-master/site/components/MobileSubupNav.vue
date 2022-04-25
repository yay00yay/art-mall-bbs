<template>
  <div class="navbar">
    <div class="navbar-item">
      <van-search v-model="searchQuery" placeholder="请输入搜索关键词" />
    </div>
    <!-- T:04200953 -->
    <div v-if="activeDomain === 'mall'" class="navbar-submenu">
      <van-tabs v-model="activeName" @click="onClickSubMenu" class="navbar-submenu-tabs">
        <van-tab title="首页" name="home"></van-tab>
        <van-tab title="最新" name="newest"></van-tab>
        <van-tab title="推荐" name="recommend"></van-tab>
      </van-tabs>
    </div>
    <div v-if="activeDomain === 'community'" class="navbar-submenu">
      <!-- <nuxt-link
        v-for="(nav, index) in config.siteNavs"
        :key="index"
        :to="nav.url"
        class="navbar-sub-item"
        >{{ nav.title }}</nuxt-link
      > -->
      <van-tabs v-model="activeName" @click="onClickSubMenu" class="navbar-submenu-tabs">
        <van-tab title="首页" name="home"></van-tab>
        <van-tab title="话题" name="topics"></van-tab>
        <van-tab title="文章" name="articles"></van-tab>
      </van-tabs>
    </div>
    <div v-if="activeDomain === 'meta'" class="navbar-submenu">
      <van-tabs v-model="activeName" @click="onClickSubMenu" class="navbar-submenu-tabs">
        <van-tab title="数字艺术" name="arts"></van-tab>
        <van-tab title="数创空间" name="spaces"></van-tab>
      </van-tabs>
      <!-- <div class="navbar-sub-item"><span>数字艺术</span></div>
      <div class="navbar-sub-item"><span>数创空间</span></div> -->
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
      navbarActive: false,
      searchQuery: ""
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
    toggleNav() {
      this.navbarActive = !this.navbarActive
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
.navbar {
  /*opacity: 0.99;*/
  /*border-bottom: 1px solid #e7edf3;*/
  background-color: var(--bg-color);

  .navbar-item {
    font-weight: 700;
  }

  .publish {
    color: var(--text-color);
    background-color: #3174dc;
    width: 100px;
    &:hover {
      color: var(--text-color);
      background-color: #4d91fa;
    }
  }

  .login-btn {
    border-color: #000; // TODO
    &:hover {
      color: var(--text-color3);
      border-color: var(--text-color3);
    }
  }
  // T:04200953
  .navbar-start {
    margin: auto;
  }

  .navbar-submenu {
    display: flex;
    padding: 0.5rem 0.75rem;
    justify-content: space-evenly;
  }

  .navbar-submenu-tabs {
    width: -webkit-fill-available;
  }
}
</style>
