<template>
  <div class="icons">
    <swiper :options="swiperOption">
        <swiper-slide v-for='(page, index) in pages' :key='index'>
            <div class="icon" v-for='item in page' :key='item.id'>
                <div class='icon-img'>
                    <img :src="item.iconUrl" class='icon-img-content' />
                </div>
                <p class='icon-desc'>{{ item.title }}</p>
            </div>
        </swiper-slide>
    </swiper>
  </div>
</template>
<script>
export default {
  name: "HomeIcons",
  data () {
      return {
          swiperOption: {
              autoplay: false
          }
      }
   },
   props: {
       iconList: Array
   },
   computed: {
       pages () {
           const pages = []
           this.iconList.forEach((item, index) => {
               const page = Math.floor(index / 8)
               if(!pages[page]) {
                   pages[page] = []
               }
               pages[page].push(item)
           })
           return pages
       }
   }
};
</script>
<style lang="stylus" scoped>
@import '~styles/varibles.styl';
@import '~styles/mixins.styl';
  *
    touch-action none
  .icons >>> .swiper-container
    height 0
    padding-bottom 50%
  .icons
    margin-top .1rem
    .icon 
        position relative
        width 25%
        height 0
        float left
        padding-bottom 25%
        .icon-img
            position absolute
            top 0
            left 0
            right 0
            bottom .44rem
            box-sizing border-box
            padding .1rem
            .icon-img-content
                display block
                margin 0 auto
                height 100%
        .icon-desc
            text-align center
            position absolute
            left 0
            right 0
            bottom .08rem
            height .44rem
            line-height .44rem
            color $darkTextColor
            font-weight 600
            ellipsis()
</style>