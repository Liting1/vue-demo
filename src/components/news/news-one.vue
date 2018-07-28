<template>
<section class="aui-middle-dome">
  <a href="javascript:;" data-action-label="click-a" data-tag="news" class="aui-middle-dome-a">
    <div class="aui-middle-dome-title">
      <h3>{{news.title}}</h3>
      <div class="aui-middle-dome-text">
        <div class="clearfix">
          <span class="aui-top box-line">置顶</span>
          <!-- <span class="aui-title">央视网新闻</span> -->
          <span class="aui-comment">评论 67890</span>
        </div>
      </div>
    </div>
    <div class="aui-middle-dome-img">
      <img :src="news.pic" alt="">
    </div>
  </a>
</section>
</template>

<script>
export default {
  name: 'news-one',
  props: {
    news: {
      type: Object
    }
  },
  data () {
    return {
    }
  },
  created () {
  }
}
</script>

<style scoped lang="stylus">
</style>
