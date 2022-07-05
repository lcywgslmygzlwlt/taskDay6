<template>
  <div>
    <p>2. 查询某本书籍信息</p>
    <input type="text" placeholder="请输入要查询 的书名" v-model="bookname" />
    <button @click="findbook">查询</button>
  </div>
</template>

<script>
import axios from 'axios';
// import { set } from 'vue/types/umd';
export default {
  data() {
    return {
      bookname: '',
      list: [],
    };
  },
  methods: {
    findbook() {
      if (this.bookname.length == 0) return alert('请重新输入');

      axios({
        url: '/api/getbooks',
        params: {
          bookname: this.bookname,
        },
      }).then((res) => {
        // console.log(res);
        this.list = res.data.data;
        this.$emit('cha', this.list);
        // this.$emit('ipt',this.bookname)
        // console.log(this.list);
        // console.log(this.list);
      });
      this.bookname=''
    },
  },
};
</script>

<style></style>
