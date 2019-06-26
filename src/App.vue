<template>
  <div id="app">
    <transition mode="out-in" appear>
      <keep-alive>
        <router-view/>
      </keep-alive>
    </transition>
  </div>
</template>

<script>
export default {

}
</script>

<style>
.v-enter,
.v-leave-to {
  transform: translateX(-100%)
}

.v-enter-active,
.v-leave-active {
  transition: all .3s ease
}
</style>
