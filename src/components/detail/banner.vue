<template>
  <div>
    <div class="banner">
        <img class="banner-img"  @click="gallary" src="http://img1.qunarzz.com/sight/p0/1703/a4/a4357d1a8afc001da3.water.jpg_600x330_0f7f8f11.jpg" />
        <div class="banner-info">
            <div class="banner-number"><span class='iconfont'>&#xe646;</span>22</div>
            <div class="banner-title">武汉东湖磨山(AAAAA景区)</div>
        </div>
    </div>
    <common-gallary 
     :imgs="imgs" 
     v-show="showGallary"
     @close="handleGallary"
    ></common-gallary>
  </div>
</template>

<script>
import CommonGallary from 'common/gallary/Gallary'
export default {
    name: "banner",
    data () {
        return {
            imgs: ['http://img1.qunarzz.com/sight/p0/1703/a4/a4357d1a8afc001da3.water.jpg_r_800x800_fd169128.jpg',
                    'http://img1.qunarzz.com/sight/p0/1703/cc/cc385156ce854a1ba3.water.jpg_r_800x800_e9485c20.jpg',
                    'http://img1.qunarzz.com/sight/p0/1703/d7/d7f80be8a44db88aa3.water.jpg_r_800x800_6c10dd86.jpg'
                  ],
            showGallary: false
        }
    },
    methods: {
        gallary () {
            this.showGallary = !this.showGallary
        },
        handleGallary () {
            this.showGallary = false
        }
    },
    components: {
        CommonGallary
    }
}
</script>

<style lang='stylus' scoped>
    .banner
        overflow hidden
        height 0
        padding-bottom 55%
        position relative
        .banner-img
            width 100% 
        .banner-info
            display flex
            flex-direction column
            padding 0 .4rem
            position absolute
            left 0
            right 0
            bottom 0
            line-height .6rem
            color #fff
            background-image linear-gradient(top, rgba(0, 0, 0, 0), rgba(0, 0, 0, 0.8))
            .banner-number
                padding 0 .4rem
                line-height .5rem
                width .6rem
                height .5rem
                border-radius .2rem
                background-color rgba(0, 0, 0, .4) 
                span 
                    font-size .23rem
                    margin-right .1rem 
            .banner-title
                flex 1
                font-size .32rem
</style>
