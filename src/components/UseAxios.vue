<template>
  <div>
    <p>1. 获取所有图书信息</p>
    <button @click="getbooks">点击-查看控制台</button>
    <p>2. 查询某本书籍信息</p>
    <input type="text" placeholder="请输入要查询 的书名" v-model="bookname" />
    <button @click="findbook">查询</button>
    <p>3. 新增图书信息</p>
    <div>
      <input type="text" placeholder="书名" v-model="bookObj.bookname" />
    </div>
    <div>
      <input type="text" placeholder="作者" v-model="bookObj.author" />
    </div>
    <div>
      <input type="text" placeholder="出版社" v-model="bookObj.publisher" />
    </div>
    <button @click="postbook">发布</button>
  </div>
</template>

<script>
import axios from 'axios';
// 目标1: 获取所有图书信息
// 1. 下载axios
// 2. 引入axios
// 3. 发起axios请求

// 4. 全局配置

export default {
  data() {
    return {
      bName: '',
      bookObj: {
        // 参数名提前和后台的参数名对上-发送请求就不用再次对接了
        bookname: '',
        author: '',
        publisher: '',
      },
      bookname: '',
    };
  },
  methods: {
    getbooks() {
      console.log(
        axios({
          url: 'http://123.57.109.30:3006/api/getbooks',
        }).then((res) => {
          console.log(res);
        })
      );
    },
    findbook() {
      axios({
        url: ' http://123.57.109.30:3006/api/getbooks',
        params: {
          bookname: this.bookname,
        },
      }).then((res) => {
        console.log(res);
      });
    },
    postbook() {
      this.axios({
        url: 'http://123.57.109.30:3006/api/addbook',
        method: 'POST',
        data: {
          appkey: '7250d3eb-18e1-41bc-8bb2-11483665535a',
          ...this.bookObj,
        },
      }).then((res) => {
        console.log(res);
      });
    },
  },
};
</script>

<style></style>
