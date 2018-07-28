<template>
<footer class="aui-bar aui-bar-tab" id="footer" style="border-top:1px solid #ddd; background:#efefef">
  <div class="aui-bar-tab-item" :class="{'aui-active': auiActive === index}" :key="item.id" v-for="(item, index) in items">
    <a href="javascript:;" @click="fotfun(index)">
      <i class="aui-iconfont" :class="'aui-icon-' + item[0]"></i>
      <div class="aui-bar-tab-label">{{item[1]}}</div>
    </a>
  </div>
</footer>
</template>

<script>
export default {
  data () {
    return {
      items: [
        ['home', '首页'],
        ['like', '要闻'],
        ['video', '视频'],
        ['my', '我的']
      ],
      auiActive: 0
    }
  },
  methods: {
    fotfun (i) {
      this.auiActive = i
    }
  }
}
</script>

<style scoped lang="stylus">
  a:hover
    text-decoration: none
</style>
