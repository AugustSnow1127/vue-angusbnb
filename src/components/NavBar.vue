<template lang="pug">
nav.navbar.navbar-expand-lg.bg-light
  router-link.navbar-brand.nav-link(to="/" tag="a")
    img#brandLogo(src="https://fxdailyreport.com/wp-content/uploads/2018/10/Atlassian-Corporation-1200x1200.png")
  button.navbar-toggler(type='button' data-toggle='collapse' data-target='#navbarNav' aria-controls='navbarNav' aria-expanded='false' aria-label='Toggle navigation')
    span.navbar-toggler-icon
  #navbarNav.collapse.navbar-collapse
    ul.navbar-nav
      li.nav-item
        router-link.nav-link(to="/" tag="a") 住宿 
          span.sr-only (current)
      li.nav-item
        a.nav-link(href='#') 機票
      li.nav-item
        a.nav-link(href='#') 租車
      li.nav-item
        a.nav-link(href='#') 熱門景點
      li.nav-item
        router-link.nav-link(to="/becomehost" tag="a") 成為房東
      li.nav-item(v-if="!showNav")
        router-link.nav-link.navBtn(to="/login" tag="a") 登入
      li.nav-item(v-else)
        .user 您好 {{ this.userProfile.lastName }}{{ this.userProfile.firstName }}
        a.nav-link.navBtn(@click="logout()") 登出
        
</template>

<script>
import { mapState } from 'vuex'

export default {
  computed: {
    ...mapState({
      userProfile: state => state.mLogin.userProfile
    }),
    showNav() {
      return Object.keys(this.userProfile).length > 0
    }
  },
  methods: {
    logout() {
      this.$store.dispatch('mLogin/logout')
      alert('您已成功登出');
    }
  }
}
</script>

<style lang="sass">
$Blue: #0051CB

li
  padding-left: 0.25rem
  font-weight: 600
  font-size: 22px
  .navBtn
    border-radius: 50px
    position: absolute
    right: 30px
    margin: 5px
    padding: 10px 30px
    border: 1px solid black
    transition: 0.2s
    width: 70px
    color: black
    background-color: white
    &:hover
      color: white
      background-color: $Blue
  .user
    position: absolute
    right: 90px
    margin: 5px
    padding: 10px 30px
    font-weight: normal
  
.nav-link
  color: black
  &:hover
    color: $Blue

.navbar-toggler
  border: 1px solid transparent
  border-radius: 0.25rem

.navbar-toggler-icon 
  background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' width='30' height='30' viewBox='0 0 30 30'%3e%3cpath stroke='rgba%280, 0, 0, 0.5%29' stroke-linecap='round' stroke-miterlimit='10' stroke-width='2' d='M4 7h22M4 15h22M4 23h22'/%3e%3c/svg%3e")

#brandLogo
  width: 40px
</style>