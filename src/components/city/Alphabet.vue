<template>
    <ul class="list">
        <li 
          class="item" 
          v-for="(item, index) in letters" 
          :key="index" 
          :ref="item"
          @touchstart="handleTouchStart"
          @touchmove="handleTouchMove"
          @touchend="handleTouchEnd"
          @click="handleClick"
        >
          {{ item }}
        </li>
    </ul>
</template>

<script>
export default {
  name: "CityAlphabet",
  props: ['city'],
  computed: {
    letters () {
      const letters = []
      for (let i in this.city) {
        letters.push(this.city[i].initial)
      }
      return letters
    }
  },
  data () {
    return {
      touchStatus: false,  //开关
      startY: 0,
      timer: null  //节流
    }
  },
  updated () {
    this.startY = this.$refs['A'][0].offsetTop //A距离上面的距离
  },
  methods: {
    handleClick(e) {
      this.$emit("change", e.target.innerText)
    },
    handleTouchStart () {
      this.touchStatus = true
    },
    handleTouchMove (e) {
      if (this.touchStatus) {
        if (this.timer) {
          clearTimeout(this.timer)
        }
        this.timer = setTimeout(() => {
            const touchY = e.touches[0].clientY - 79 //手指距离最顶部的高度
            const index = Math.floor((touchY - this.startY) / 20)  //20为字母高度 取整获得下标
            if (index >= 0 && index < this.letters.length) {
              this.$emit("change", this.letters[index])
            }
        }, 16);
      }
    },
    handleTouchEnd () {
      this.touchStatus = false
    },
  }
}
</script>

<style lang='stylus' scoped>
  @import '~styles/varibles.styl'
  .list
    display flex
    flex-direction column
    justify-content center
    position absolute
    top 1.58rem
    right 0
    bottom 0
    width .4rem
    .item
      text-align center
      line-height .4rem
      color $bgColor
</style>