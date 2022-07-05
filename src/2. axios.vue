<template>
  <div>
    <h1>2. axios使用</h1>
    <UseAxios></UseAxios>
  </div>
</template>

<script>
import UseAxios from './components/UseAxios.vue'
export default {
  data() {
    return {
      isShow: true,
    }
  },
  components: {
    UseAxios,
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
