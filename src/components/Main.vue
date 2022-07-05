<template>
  <div>
    <Title @newList="newListFn" @returns="returnsFn"></Title>

    <table border="1" cellpadding="10" cellspacing="0">
      <tr>
        <th>序号</th>
        <th>书名</th>
        <th>作者</th>
        <th>出版商</th>
        <th>操作</th>
      </tr>
      <tr v-for="obj in list" :key="obj.id">
        <td>{{ obj.id }}</td>
        <td>{{ obj.bookname }}</td>
        <td>{{ obj.author }}</td>
        <td>{{ obj.publisher }}</td>
        <td>
          <button @click="del(obj.id)">删除</button>
          <button @click="isAll(obj.id)">详情</button>
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
import Title from './Title.vue';

export default {
  components: {
    Title,
  },
  data() {
    return {
      list: [],
    };
  },
  created() {
    this.addList();
  },
  methods: {
    addList() {
      this.$axios({
        url: '/api/getbooks',
      }).then((res) => {
        // console.log(res.data.data);
        this.list = res.data.data;
      });
    },
    newListFn(val) {
      // console.log(val)
      this.list = val;
    },
    returnsFn(val) {
      // console.log(val);
      this.list = val;
    },
    del(val) {
      // console.log(val);
      this.$axios({
        url: '/api/delbook',
        params: { id: val },
      }).then(() => {
        this.addList();
      });
    },
    isAll(val) {
      // console.log(val);
      this.$axios({
        url: '/api/getbooks',
        params: { id: val },
      }).then((res) => {
        // console.log(res);
        alert(
          `书名：${res.data.data[0].bookname},\n作者：${res.data.data[0].author},\n出版社：${res.data.data[0].publisher}`
        );
      });
    },
  },
};
</script>

<style>
th {
  padding: 10px 30px;
}

td {
  text-align: center;
}
</style>
