<template>
  <div class="container">
    <div class="navbar-end">
      <div class="navbar-item">
        <search-input />
      </div>
    </div>
    <!-- T:04200953 -->
    <div v-if="activeDomain === 'mall'" class="navbar-submenu">
      <div class="navbar-sub-item"><span>首页</span></div>
      <div class="navbar-sub-item"><span>最新</span></div>
    </div>
    <div v-if="activeDomain === 'community'" class="navbar-submenu">
      <nuxt-link
        v-for="(nav, index) in config.siteNavs"
        :key="index"
        :to="nav.url"
        class="navbar-sub-item"
        >{{ nav.title }}</nuxt-link
      >
    </div>
    <div v-if="activeDomain === 'meta'" class="navbar-submenu">
      <div class="navbar-sub-item"><span>数字艺术</span></div>
      <div class="navbar-sub-item"><span>数创空间</span></div>
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
    position: absolute;
    top: 70px;
    display: flex;
  }

  .navbar-sub-item {
    margin: auto 1rem;
  }

  .nav-domain {
    margin: auto;
  }

  .nav-domain ul {
    display: flex;
  }
}

.user-menus {
  .user-menus-nickname {
    margin-left: 5px;
  }
}
</style>
