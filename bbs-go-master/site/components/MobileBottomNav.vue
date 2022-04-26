<template>
  <div class="navbar">
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
          <nuxt-link :to="'/meta/arts'">
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
  },
}
</script>

<style lang="scss" scoped>
.navbar {
  /*opacity: 0.99;*/
  /*border-bottom: 1px solid #e7edf3;*/
  background-color: var(--bg-color);
  position: fixed;
  bottom: 0px;
  left: 0px;
  right: 0px;
  z-index: 30;

  .navbar-item {
    font-weight: 700;
  }

  .nav-domain {
    margin: auto;
  }

  .nav-domain ul {
    display: flex;
    justify-content: space-evenly;
  }
}
</style>
