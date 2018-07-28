<template>
<section class="aui-middle-dome">
  <a href="javascript:;" data-action-label="click-a" data-tag="news" class="aui-middle-dome-a">
    <div class="aui-middle-dome-title" style="width: 100%">
      <h3>{{news.title}}</h3>
      <div v-if="news.pic" class="aui-middle-dome-img" style="width: 100%; margin-top: 12px">
        <img :src="news.pic" alt="">
      </div>
      <div class="aui-middle-dome-text">
        <div class="clearfix">
          <span class="aui-top box-line">置顶</span>
          <!-- <span class="aui-title">央视网新闻</span> -->
          <span class="aui-comment">评论 67890</span>
        </div>
      </div>
    </div>
  </a>
</section>
</template>

<script type="text/javascript">
export default {
  name: 'news-two',
  props: {
    news: {
      type: Object
    }
  }
}
</script>

<style>
</style>
