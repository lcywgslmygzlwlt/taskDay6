<template>
  <div>
    <p>获取图书信息</p>
    <button @click="getBook">查看信息</button>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  data() {
    return {
      Objbook: {
        bookname: '',
        author: '',
        publisher: '',
        id: '',
      },
    };
  },

  methods: {
    getBook() {
      this.$axios({
        url: '/api/getbooks',
        method: 'GET',
      }).then((res) => {
        console.log(res);
      });
    },
  },
};
</script>

<style></style>
