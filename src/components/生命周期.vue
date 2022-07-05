<template>
  <div>
    <p>学习生命周期 - 看控制台打印</p>
    <p id="myP">{{ msg }}</p>
    <ul id="myUL">
      <li v-for="item in arr" :key="item">{{ item }}</li>
    </ul>

    <button @click="arr.push(1000)">点击末尾加值</button>
  </div>
</template>

<script>
export default {
  name: 'LifeAxiosLife',
  data() {
    return {
      msg: 'Hello Vue!',
      arr: [1, 2, 3, 4],
      tiemr: '',
    };
  },
  beforeCreate() {
    console.log('beforeCreate执行了');
    console.log(this.msg); //undefined
    // this.fn(); //报错 在刚开始创建时 还没有完成数据初始化
  },
  created() {
    console.log('created执行了');
    console.log(this.msg); //Hello Vue!
    this.fn(); //111
    // this.tiemr = setInterval(() => {
    //   console.log(111);
    // }, 1000);
  },
  beforeMount() {
    console.log('beforeMount执行了');
    console.log(document.querySelector('p'));
    // 挂载前 不可以操作dom元素
  },
  mounted() {
    console.log('mounted执行了');
    console.log(document.querySelector('p'));
    // 挂载后 可以操作dom元素
  },
  beforeUpdate() {
    console.log('beforeUpdate执行了');
    console.log(this.arr[4]);
    console.log(document.querySelectorAll('#myUL >li')[4]);
    // 数据更新 页面不更新
  },
  updated() {
    console.log('updated执行了');
    console.log(this.arr[4]);
    console.log(document.querySelectorAll('#myUL >li')[4]);
    // 数据更新 页面更新
  },
  beforeDestroy() {
    console.log('beforeDestroy执行了');
    console.log(this.msg);
    clearInterval(this.tiemr);
  },
  destroyed() {
    console.log('destroyed执行了');
    console.log(this.msg);
  },
  methods: {
    fn() {
      console.log(111);
    },
  },
};
</script>

<style scoped></style>
