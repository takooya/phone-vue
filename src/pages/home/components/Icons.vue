<template>
  <div class="icons">
    <swiper :options="swiperOption">
      <swiper-slide v-for="(page,index) of pages" :key="index">
        <div class="icon" v-for="item of page" v-bind:key="item.id">
          <div class="icon-img"><img class="icon-img-content" :src="item.imgUrl"/></div>
          <p class="icon-desc">{{item.desc}}</p>
        </div>
      </swiper-slide>
    </swiper>
  </div>
</template>

<script>
import HomeSwiper from './Swiper'

export default {
  name: 'HomeIcons',
  props: {
    list: {
      type: Array,
      default: function () {
        return [{
          id: '0001',
          imgUrl: 'http://img1.qunarzz.com/piao/fusion/1803/95/f3dd6c383aeb3b02.png',
          desc: '暂无数据'
        }]
      }
    }
  },
  components: {HomeSwiper},
  data () {
    return {
      swiperOption: {
        autoplay: false
      }
    }
  },
  computed: {
    pages () {
      const pages = []
      this.list.forEach((item, index) => {
        const page = Math.floor(index / 8)
        if (!pages[page]) {
          pages[page] = []
        }
        pages[page].push(item)
      })
      return pages
    }
  }
}
</script>

<style lang="stylus" scoped>
@import "~styles/varibles.styl"
@import "~styles/mixins.styl"
.icons >>> .swiper-container
  height: 0
  padding-bottom: 50%

.icons
  margin-top: 5px
  margin-bottom: 5px

  .icon
    position: relative
    overflow: hidden
    height: 0
    width: 25%
    float: left
    padding-bottom: 25%

    .icon-img
      position: absolute
      top: 0
      left: 0
      right: 0
      bottom: 24px
      background: white
      box-sizing: border-box
      padding: 1px

      .icon-img-content
        height: 100%
        display: block
        margin: 0 auto

    .icon-desc
      position: absolute
      left: 0
      right: 0
      bottom: 0
      line-height: 24px
      height: 24px
      color: $darkTextColor
      text-align: center
      ellipsis()

</style>
