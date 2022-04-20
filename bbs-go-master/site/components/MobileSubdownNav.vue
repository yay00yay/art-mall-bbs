<template>
  <div class="container">
    <!-- T:04200953 -->
    <div class="nav-domain">
      <ul>
        <li
          :class="{ 'is-active': activeDomain === 'mall' }"
          class="navbar-item"
        >
          <nuxt-link :to="'/mall'">
            <span>商城</span>
          </nuxt-link>
        </li>
        <li
          :class="{ 'is-active': activeDomain === 'community' }"
          class="navbar-item"
        >
          <!-- T:04200953 default: / belongs to to community-->
          <nuxt-link :to="'/'">
            <span>社区</span>
          </nuxt-link>
        </li>
        <li
          :class="{ 'is-active': activeDomain === 'meta' }"
          class="navbar-item"
        >
          <nuxt-link :to="'/meta'">
            <span>星球</span>
          </nuxt-link>
        </li>
      </ul>
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
