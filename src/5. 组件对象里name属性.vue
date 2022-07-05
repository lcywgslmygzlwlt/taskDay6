<template>
  <div>
    <h1>5. 组件对象里name属性</h1>
    <ComNameHaHa></ComNameHaHa>
  </div>
</template>

<script>
import Com from './components/Com.vue'
export default {
  data() {
    return {
      isShow: true,
    }
  },
  components: {
    Com,
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
