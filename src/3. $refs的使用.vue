<template>
  <div>
    <h1>3. $refs的使用</h1>
    <More></More>
  </div>
</template>

<script>
import More from './components/More.vue'
export default {
  data() {
    return {
      isShow: true,
    }
  },
  components: {
    More,
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
