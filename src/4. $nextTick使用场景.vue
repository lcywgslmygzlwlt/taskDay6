<template>
  <div>
    <h1>4. $nextTick使用场景</h1>
    <Tick></Tick>
  </div>
</template>

<script>
import Tick from './components/Tick.vue'
export default {
  data() {
    return {
      isShow: true,
    }
  },
  components: {
    Tick,
  },
  methods: {
    clickFn() {
      this.isShow = false
      setTimeout(() => {
        console.log(this.$refs.mylife)
      }, 3000)
    },
  },
}
</script>

<style></style>
