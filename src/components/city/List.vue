<template>
  <div class='list' ref="wrapper">
    <div>
        <div class="area">
            <div class="title border-topbottom">当前城市</div>
            <div class="button-list">
                <div class="button-wrapper">
                    <div class="button">{{ this.$store.getters.city }}</div>
                </div>            
            </div>
        </div>
        <div class="area">
            <div class="title border-topbottom">热门城市</div>
            <div class="button-list">
                <div class="button-wrapper" v-for="(item, index) in hot" :key="index" @click="cityClick(item.name)">
                    <div class="button">{{ item.name }}</div>
                </div>            
            </div>
        </div>
        <div class="area" 
             v-for="(item, index) in city" 
             :key="index"
             :ref="item.initial"
        >
            <div class="title border-topbottom">{{ item.initial }}</div>
            <div class="item-list">
                <div class="item border-bottom" 
                     v-for="(i, index) in item.list" 
                     :key="index"
                     @click="cityClick(i.name)"
                >
                    {{ i.name }}
                </div>
            </div>
        </div>
        
    </div>
  </div>
</template>

<script> 
import Bscroll from "better-scroll"
import { mapState, mapMutations } from "vuex"
export default {
  name: "CityList",
  props: ['hot','city','letter'],
  computed: {
      ...mapState ({
          currentCity: "city"
      })
  },
  methods: {
      cityClick (city) {
        //  this.$store.commit("changeCity", city)
         this.changeCity(city)
		 this.$router.push('/')
      },
      ...mapMutations (["changeCity"])
  },
  watch: {
      letter() {
          if (this.letter) {
              const element = this.$refs[this.letter][0]
              this.scroll.scrollToElement(element)
          }
      }
  },
  mounted() {
      this.scroll = new Bscroll(this.$refs.wrapper, { click: true })
  }
}
</script>

<style lang='stylus' scoped>
  @import '~styles/varibles.styl'
  .border-topbottom
      &:before
          border-color #ccc
      $:after
          border-color #ccc
  .border-bottom
      &:before
          border-color #ccc
  .list
    overflow hidden
    position absolute
    top: 1.58rem
    left: 0
    right: 0
    bottom 0
    .title
        line-height .54rem
        background #eee
        padding-left .2rem
        color #666
        font-size .26rem
    .button-list
        padding .1rem .6rem .1rem .1rem
        overflow hidden
        .button-wrapper
            width 33.33%
            float left
            .button 
                text-align center
                margin .1rem .1rem
                border .02rem solid #ccc
                padding .1rem 0
                border-radius .06rem 
    .item-list
        .item
            line-height .76rem
            padding-left .2rem
</style>