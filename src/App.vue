<template>
  <div id="app">
    <div class="header">
      <v-header></v-header>
    </div>
    <div class="content">
      <v-content></v-content>
    </div>
    <div class="footer">
      <v-footer></v-footer>
    </div>
  </div>
</template>

<script>
import header from './components/header/header.vue'
import content from './components/content/content'
import footer from './components/footer/footer'
export default {
  name: 'App',
  data () {
    return {
      now: false
    }
  },
  components: {
    'v-header': header,
    'v-content': content,
    'v-footer': footer
  },
  methods: {
    hide () {
      this.now = false
    }
  }
}
</script>

<style scoped lang="stylus">
#app
  width: 100%;
  height: 100%;
  .header
    width: 100%
    height: 84px
    position: fixed
    top: 0
    left: 0
    z-index: 2
  .content
    width: 100%
    position: fixed
    top: 84px
    bottom: 50px
    background-color: #fff
    z-index: 1
  .footer
    width: 100%
    // height: 50px
    position: fixed
    bottom: 0
    left: 0
    background-color: greenyellow
    z-index: 2
</style>
