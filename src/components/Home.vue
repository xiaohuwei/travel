<template>
  <div class="hello">
    <home-header></home-header>
    <home-swiper :swiperList="swiperList"></home-swiper>
    <home-icons :iconList="iconList"></home-icons>
    <home-recommend :recommendList="recommendList"></home-recommend>
    <home-weekend :weekendList="weekendList"></home-weekend>
  </div>
</template>

<script>
import HomeHeader from './home/Header'
import HomeSwiper from './home/Swiper'
import HomeIcons from './home/Icons'
import HomeRecommend from './home/Recommend'
import HomeWeekend from './home/Weekend'
import axios from 'axios'
import { mapState } from 'vuex'
export default {
  components: {
    HomeHeader,
    HomeSwiper,
    HomeIcons,
    HomeRecommend,
    HomeWeekend
  },
  data() {
    return {
      swiperList: [],   //首页轮播图
      iconList: [],   //首页icon
      recommendList: [],  //热销推荐
      weekendList: [],  //周末去哪儿
      lastCity: ''
    }
  },
  computed: {
    ...mapState(['city'])
  },
  methods: {
    getData() {
      axios
      .get('http://rest.apizza.net/mock/017115113699d51c0ac8ed8053936d81/travel/?city=' + this.city)
      .then((res) => {
        const data = res.data.data
        if(data.ret) {
          this.swiperList = data.swiperList
          this.iconList = data.iconList
          this.recommendList = data.recommendList
          this.weekendList = data.weekendList
        }
      })
    }
  },
  mounted() {
    this.lastCity = this.city
    this.getData()
  },
  activated () {
    if (this.lastCity !== this.city) {
      this.lastCity = this.city
      this.getData()
    }
  }
}
</script>

<style lang='stylus' scoped>
  // * {
  //   touch-action none
  // }
</style>
