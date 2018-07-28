<template>
  <div class="header">
    <div class="header-top">
      <div class="header-logo">
        <img src="../../assets/img/logo.png" alt="logo">
      </div>
      <div class="header-search">
        <i class="aui-iconfont aui-icon-search"></i>
      </div>
    </div>
    <div class="header-nav" ref="headerNav">
      <ul ref="listBox">
        <li :class="{active: active == index}" :key="item.id" @click="swtFun(index)" v-for="(item, index) in items"><a href="javascript:;">{{ item }}</a></li>
      </ul>
    </div>
  </div>
</template>

<script>
import BScroll from 'better-scroll'
import bus from '../../assets/js/event.js'

export default {
  data () {
    return {
      items: ['推荐', '视频', '热点', '社会', '娱乐', '军事', '科技', '体育', '财经', '国际', '时尚'],
      active: ''
    }
  },
  methods: {
    automatic () {
      let w = document.documentElement.clientWidth
      let ul = this.$refs.listBox
      let liArr = ul.children
      let liLen = liArr.length
      ul.style.width = (w / 5.5) * liLen + 'px'
      for (let i = 0; i < liLen; i++) {
        liArr[i].style.width = (w / 5.5) + 'px'
      }
    },
    swtFun (index) {
      this.active = index
      // 借用一个新的Vue实例来进行组件之间的事件通信
      bus.$emit('onchange', index)
    }
  },
  computed: {},
  created () {
    this.$nextTick(() => {
      this.automatic()
      if (!this.scrollNav) {
        this.scrollNav = new BScroll(this.$refs.headerNav, {
          click: true,
          scrollX: true,
          bounceTime: 400 // 设置轮动的弹回动画
        })
      }
    })
  },
  mounted () {
    window.onresize = () => {
      this.automatic()
    }
  },
  components: {}
}
</script>

<style scoped lang="stylus">
  .header
    .header-top
      padding: 0 15px
      box-sizing: border-box
      height: 44px
      background-color: #d43d3d
      .header-logo
        width: 100px
        float: left
        margin-top: 8.67px
        img
          width: 100%
      .header-search
        float: right
        color: #fff
        line-height: 44px
        i
          font-size: 18px
          font-weight: 800
    .header-nav
      width: 100%
      height: 40px
      box-sizing: border-box
      overflow: hidden
      background-color: #efefef
      position: relative
      top: -1px
      ul
        display: flex
        height: 40px;
        li
          text-align: center
          a
            line-height: 40px
            font-size: 14px
            color: #212121
            font-family: "Helvetica Neue", Helvetica, sans-serif
            &:hover
              text-decoration: none
        li.active a
          color: #ec5566
</style>
