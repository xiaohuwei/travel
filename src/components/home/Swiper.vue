<template>
  <div class='wrapper'>
    <swiper :options="swiperOption" v-if="showSwiper">
      <swiper-slide v-for='item in swiperList' :key='item.id'>
        <img class="swiper-img" :src="item.imgUrl">
      </swiper-slide>
      <div class="swiper-pagination" slot="pagination"></div>
    </swiper>
  </div>
</template>

<script>
export default {
  name: "HomeSwiper",
  data() {
    return {
      swiperOption: {
          pagination: '.swiper-pagination',
          loop: true,
          autoplay: 3000,
          autoplayDisableOnInteraction: false
      }
    }
  },
  props: {
    swiperList: Array
  },
  computed: {
    showSwiper () {
      return this.swiperList.length
    }
  }
};
</script>

<style lang="stylus" scoped>
    .wrapper >>> .swiper-pagination-bullet-active
        background-color #fff
    .wrapper
        overflow hidden
        width 100%
        height 0
        padding-bottom 26.8%
        background-color #eee
        .swiper-img 
            width: 100%
    
</style>