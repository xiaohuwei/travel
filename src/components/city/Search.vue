<template>
    <div>
			<div class="search">
				<input v-model="keyword" class="search-input" type="text" placeholder="输入城市名或拼音" />
			</div>
			<div 
				class="search-content" 
				ref="search"
				v-show="keyword"
			>
				<ul>
					<li class="search-item border-bottom" 
							v-for="(item, index) in list" 
							:key="index"
							@click="cityClick(item)"
					>
						{{ item }}
					</li>
					<li class="search-item border-bottom" v-show="hasNoData">
						没有找到匹配数据
					</li>
				</ul>
			</div>
    </div>
</template>
<script>
import Bscroll from 'better-scroll'
import { mapMutations } from 'vuex';
export default {
		name: "CitySearch",
		props: ["city"],
		data () {
			return {
				keyword: "",
				list: [],
				timer: null
			}
		},
		computed: {
			hasNoData () {
				return !this.list.length
			}
		},
		watch: {
			keyword () {
				if (this.timer) {
					clearTimeout(this.timer)
				}
				if (!this.keyword) {
					this.list = []
					return
				}
				this.timer = setTimeout(() => {
					const result = []
					for (let i in this.city) {
						this.city[i].list.forEach((value) => {
							value.pinyin = value.pinyin.toLowerCase()  //全部换为小写
							if (value.pinyin.indexOf(this.keyword) > -1 || 
							    value.name.indexOf(this.keyword) > -1) {
										result.push(value.name)
							}
						})
					}
					this.list = result
				}, 100);
			}
		},
		methods: {
			cityClick (city) {
				//  this.$store.commit("changeCity", city)
				this.changeCity(city)
				this.$router.push('/')
			},
			...mapMutations (["changeCity"])
		},
		mounted () {
			this.scroll = new Bscroll(this.$refs.search, { click: true })
		}
}
</script>
<style lang="stylus" scoped>
    @import '~styles/varibles.styl'
    .search
        height .7rem
        background $bgColor
        padding 0 .1rem
        .search-input
            padding 0 .1rem
            box-sizing border-box
            height .62rem
            line-height .62rem
            width 100%
            text-align center
            border-radius .06rem 
            color #666
		.search-content
			overflow hidden
			position absolute
			top 1.58rem
			left 0
			right 0
			bottom 0
			background-color #eee
			z-index 1
			.search-item
				line-height .62rem
				padding-left	.2rem
				background #fff
				color #666
</style>