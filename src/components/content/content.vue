<template>
  <div class="content" ref="content">
    <div class="content-box">
      <div class="news-pages" :key="item.id" v-for="(item, index) in items" @click="showNews(index)">
        <news-one v-if="index % 2 == 0" :news="item"></news-one>
        <news-two v-if="index % 2 == 1" :news="item"></news-two>
      </div>
      <p v-show="isShow" style='text-align: center'>正在加载中...</p>
    </div>
    <div class="newsNow" v-show="isNews">
    </div>
  </div>
</template>

<script>
import BScroll from 'better-scroll'
import bus from '../../assets/js/event.js'
import newsOne from '../news/news-one'
import newsTwo from '../news/news-two'

export default {
  data () {
    return {
      items: [],
      toggle: true,
      dom: '',
      isShow: false,
      isNews: false
    }
  },
  methods: {
    receive () {
      let self = this
      bus.$on('onchange', function (i) {
        // 设置滚动位置默认为顶部
        self.scrollContent.scrollTo(0, 0)
        self.sendRequest(i)
      })
    },
    sendRequest (i) {
      this.$http.get('../../../static/data.json').then((res) => {
        this.items = res.data[i] // 获取请求数据
        if (!this.scrollContent) {
          setTimeout(() => {
            this.scrollContent = new BScroll(this.$refs.content, {
              click: true, // 派发点击事件
              scrollY: true, // 滚动的方向为Y方向
              probeType: 2 // 派发滚动事件
            })
            // console.log(this.scrollContent.maxScrollY)
            // 无限加载
            this.scrollContent.on('scroll', (pos) => {
              if (((pos.y + 50) <= this.scrollContent.maxScrollY) && this.toggle) {
                this.loadings()
                // console.log(this.scrollContent.maxScrollY)
              }
            })
          }, 20)
        } else {
          this.scrollContent.refresh()
        }
      })
    },
    loadings () {
      if (!this.toggle) return
      this.$http.get('../../../static/data.json', {
        before () {
          // 防止请求次数过多
          this.toggle = false
          this.isShow = true
        }
      }).then((res) => {
        this.items = this.items.concat(res.data[1])
        // alert(1)
        // 重载滚动元素
        setTimeout(() => {
          console.log('执行重载')
          this.scrollContent.refresh()
        }, 20)

        setTimeout(() => {
          this.toggle = true
          this.isShow = false
        }, 600)
      })
    },
    showNews (i) {
      this.isNews = true
      console.log(i)
    }
  },
  created () {
    this.sendRequest(0) // 初始数据为第一页
  },
  mounted () {
    this.receive()
  },
  components: {
    'news-one': newsOne,
    'news-two': newsTwo
  }
}
</script>

<style scoped lang="stylus">
  .content
    width: 100%
    position: relative
    .content-box
      height: auto
    .newsNow
      position: absolute
      width: 100%
      height: 100%
      top: -1px
      left: 0
      z-index: 10
      background-color red
</style>
