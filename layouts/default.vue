<template>
  <v-app >
    <v-container class="main-bg" fluid="">
    <v-navigation-drawer
      temporary
      v-model="drawer"
      disable-resize-watcher
      disable-route-watcher
      fixed
      width="256"
      app
    >
      <v-list>
        <v-list-tile
          router
          :to="item.to"
          @click="navigate(item.outlink, item.to)"
          :key="i"
          v-for="(item, i) in items"
          exact
        >
          <v-list-tile-action>
            <v-icon v-html="item.icon"></v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title v-text="item.title"></v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
    <v-toolbar class="d-flex" color="primary" dark dense flat app>
      <nuxt-link to="/">
        <v-toolbar-title>
          <v-avatar tile>
            <img src="https://user-images.githubusercontent.com/21119252/34459239-16407fee-ee1d-11e7-94c1-dc6446f962b0.png" alt="FLS Logo">
          </v-avatar>
        </v-toolbar-title>
      </nuxt-link>
      <v-spacer></v-spacer>
      <div class="align-center hidden-sm-and-down" style="margin-left: auto">
        <template v-for="item in items" >
          <v-btn v-if="item.outlink" outline round :href="item.to" :key="item.title">
            {{ item.title }}
            <v-icon size="medium" class="ml-1">{{ item.icon }}</v-icon>
          </v-btn>
          <v-btn v-else outline round :to="item.to" :key="item.title">
            {{ item.title }}
            <v-icon size="medium" class="ml-1">{{ item.icon }}</v-icon>
          </v-btn>
        </template>
      </div>
      <v-btn
        icon
        class="hidden-md-and-up"
        @click.stop="drawer = !drawer"
      >
        <v-icon>menu</v-icon>
      </v-btn>
    </v-toolbar>
    <v-content>
      <v-container>
        <nuxt />
      </v-container>
    </v-content>
    </v-container>
    <v-footer color="primary" dark flat>
      <span>
        &copy; {{ new Date().getUTCFullYear() }} — <a href="https://github.com/creativefls/" class="white--text"><strong>CreativeFLS</strong></a>
      </span>
    </v-footer>    
  </v-app>
</template>

<script>
  export default {
    data() {
      return {
        title: 'Vuetify.js',
        clipped: false,
        drawer: false,
        fixed: false,
        items: [
          { icon: 'home', title: 'Home', to: 'https://futureleadersummit.org', outlink: true },
          { icon: 'history', title: 'Riwayat', to: '/riwayat', outlink: false }
        ]
      }
    },
    methods: {
      navigate (isOut, link) {
        if (isOut) {
          window.location.href = link
        } else {
          this.$router.push(link)
        }
      }
    }
  }
</script>

<style lang="stylus">
.main-bg
  background linear-gradient(rgba(0, 0, 0, 0.7), rgba(0, 0, 0, 0.4)), url('/images/background.svg') no-repeat;
  background-size cover
nav
  justify-content center
  padding 6px 0
  .toolbar__content
    @media only screen and (min-device-width: 960px)
      max-width 80%
  .toolbar__title
    margin-left 0
    .avatar.avatar--tile
      height 36px !important
      width auto !important
  .btn
    text-transform capitalize
    font-size 16px

</style>
