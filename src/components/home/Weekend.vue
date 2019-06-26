<template>
    <div>
        <div class="title">周末去哪儿</div>
        <ul>
            <li class='item border-bottom' v-for='item in weekendList' :key='item.id'>
                <div class='item-img-wraaper'>
                    <img class='item-img' :src="item.imgUrl" />
                </div>
                <div class='item-info'>
                    <p class='item-title'>{{ item.title }}</p>
                    <p class='item-desc'>{{ item.desc }}</p>
                </div>
            </li>
        </ul>
    </div>
</template>
<script>
export default {
    name: 'HomeWeekend',
    props: {
        weekendList: Array
    },
    data () {
        return {}
    }
}
</script>
<style lang='stylus' scoped>
    @import '~styles/mixins.styl'
    .title 
        line-height .8rem
        background-color #eee
        text-indent .2rem
    .item-img-wraaper
        height 0
        overflow hidden
        padding-bottom 33.9%
        .item-img
            width 100%
    .item-info
        padding .1rem
        .item-title
            line-height .54rem
            font-size .3rem
            ellipsis()
        .item-desc
            line-height .4rem
            font-size .2rem
            ellipsis()
</style>
