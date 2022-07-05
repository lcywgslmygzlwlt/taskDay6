<template>
  <div>
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
    <chaxun @cha="cha" />
    <!-- <list /> -->
    <table border="1" cellpadding="10" cellspacing="0">
      <tr>
        <th>序号</th>
        <th>书名</th>
        <th>作者</th>
        <th>出版社</th>
        <th>操作</th>
      </tr>
      <tr v-for="obj in arr" :key="obj.id">
        <td>{{ obj.id }}</td>
        <td>{{ obj.bookname }}</td>
        <td>{{ obj.author }}</td>
        <td>{{ obj.publisher }}</td>
        <td><button @click="del(obj.id)">删除</button></td>
      </tr>
    </table>
  </div>
</template>

<script>
import chaxun from './components/title.vue';
export default {
  data() {
    return {
      arr: [],
      bookObj: {
        // 参数名提前和后台的参数名对上-发送请求就不用再次对接了
        bookname: '',
        author: '',
        publisher: '',
      },
    };
  },
  components: { chaxun },
  created() {
    this.$axios({
      url: '/api/getbooks',
    }).then((res) => {
      this.arr = res.data.data;
    });
  },
  methods: {
    cha(val) {
      console.log(val);
      alert(val[0].bookname + ',' + val[0].author + ',' + val[0].publisher);
    },
    postbook() {
      this.$axios({
        url: '/api/addbook',
        method: 'POST',
        data: {
          ...this.bookObj,
        },
      }).then((res) => {
        console.log(res);
        this.arr.push(res.data);
      });
    },
    del(id) {
      this.$axios({
        url: '/api/delbook',
        params: { id: id },
      }).then(() => {
        alert('删除成功');
      });
    },
  },
  watch: {
    arr: {
      deep: true,
      handler() {
        this.$axios({
          url: '/api/getbooks',
        }).then((res) => {
          this.arr = res.data.data;
        });
      },
    },
  },
};
</script>

<style></style>
