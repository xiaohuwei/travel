<template>
  <div class="detail">
      <detail-banner></detail-banner>
      <detail-header></detail-header>
      <div class="content"></div>
  </div>
</template>

<script>
import detailBanner from "./detail/banner"
import detailHeader from "./detail/Header"
export default {
    name: "detail",
    data () {
        return {
            id: this.$route.params.id,
        }
    },
    components: {
        detailBanner,
        detailHeader
    }
}
</script>

<style lang='stylus' scoped>
    .content
        height 50rem
</style>
