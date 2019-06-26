<template>
    <div>
        <router-link 
            to="/" 
            tag="div" 
            class="header-abs"
            v-show="showAbs"
        >
            <div class='iconfont header-abs-back'>&#xe624;</div>
        </router-link>    
        <div 
            class="header-fixed" 
            v-show="!showAbs"
            :style="opacityStyle"    
        >
            <router-link to="/">
                <div class='iconfont header-fixed-back'>&#xe624;</div>
            </router-link> 
            景点详情    
        </div>   
    </div>
</template>
<script>
export default {
    name: "detail-header",
    data () {
        return {
            showAbs: true,
            opacityStyle: {
                opacity: 0
            }
        }
    },
    methods: {
        handlerScrool () {
            console.log("scrool");
            const top = document.documentElement.scrollTop;
            if (top > 60) {
                let opacity = top / 140
                opacity = opacity > 1 ? 1 : opacity
                this.opacityStyle = { opacity }
                this.showAbs = false
            } else {
                this.showAbs = true
            }
        }
    },
    activated () {
        window.addEventListener('scroll', this.handlerScrool)
    },
    deactivated () {
        window.removeEventListener('scroll', this.handlerScrool) //解绑全局事件
    }
}
</script>
<style lang="stylus" scoped>
    @import '~styles/varibles.styl'
    .header-abs
        text-align center
        line-height .8rem
        position absolute
        left .2rem
        top .2rem
        width .8rem
        height .8rem
        border-radius .4rem
        background rgba(0, 0, 0, .8)
        .header-abs-back
            color #fff
            font-size .4rem
    .header-fixed
        height $headerHeight
        line-height $headerHeight
        text-align center
        color #fff
        background-color $bgColor
        font-size .28rem
        position fixed 
        top 0
        left 0
        right 0
    .header-fixed-back
        position absolute
        top 0
        left 0
        width .64rem
        text-align center
        font-size .4rem
        color #fff

</style>