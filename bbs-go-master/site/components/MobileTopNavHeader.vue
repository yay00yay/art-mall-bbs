<template>
  <van-row>
    <van-col span="21"><van-search v-model="searchQuery" placeholder="请输入搜索关键词" /></van-col>
    <van-col span="3">
      <div class="navbar-cart" @click="onClickCart">
        <van-icon name="cart-o" size="30px"></van-icon>
      </div>
  </van-row>
</template>

<script>
import UserHelper from '~/common/UserHelper'

export default {
  data() {
    return {
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
    onClickCart(){
      this.$linkTo("/mall/cart")
    }
  },
}
</script>

<style lang="scss" scoped>
.navbar-cart {
  padding: 10px 3px;
}
</style>