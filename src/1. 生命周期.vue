<template>
  <div>
    <h1>1. 生命周期</h1>
    <Life v-if="isShow" ref="mylife"></Life>
    <button @click="clickFn">销毁组件</button>
  </div>
</template>

<script>
import Life from './components/Lfe.vue'
export default {
  data() {
    return {
      isShow: true,
    }
  },
  components: {
    Life,
  },
}
</script>

<style></style>
