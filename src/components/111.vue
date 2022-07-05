<template>
  <div>
    <ax />
    <!-- <dome ref="mydome" /> -->
    <!-- <p ref="myp">吱吱吱吱</p> -->
    <!-- <p>{{ count }}</p> -->
    <!-- <button @click="btn">点击++</button> -->
    <!-- <tick /> -->
  </div>
</template>

<script>
import dome from './components/Child/Demo.vue';
import ax from './components/UseAxios.vue';
import tick from './components/Tick.vue';
export default {
  data() {
    return {
      count: 0,
    };
  },
  methods: {
    btn() {
      this.count++;
      console.log(this.count);
      this.$nextTick(() => {
        console.log(this.count);
        console.log(this.$refs.myp.innerHTML);
      });
    },
  },
  components: {
    ax,
    tick,
    dome,
  },
  mounted() {
    console.log(this.$refs.mydome);
    this.$refs.mydome.fn();
  },
};
</script>

<style></style>
