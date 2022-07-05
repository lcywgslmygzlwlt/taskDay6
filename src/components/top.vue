<template>
  <div id="app">
    <div id="Navigation">
      <div class="search">
        <input
          type="text"
          placeholder="搜索-书名名称"
          @keydown.enter="search"
          v-model.trim="bookname"
        />
      </div>
      <div class="add">
        <input type="text" placeholder="书名" v-model="bookObj.bookname" />
        <input type="text" placeholder="作者" v-model="bookObj.author" />
        <input type="text" placeholder="出版商" v-model="bookObj.publisher" />
        <button @click="addBook">新增</button>
      </div>
    </div>
    <table class="book" border="1" cellspacing="0" cellpadding="0">
      <tr>
        <th>序号</th>
        <th>书名</th>
        <th>作者</th>
        <th>出版商</th>
        <th>操作</th>
      </tr>
      <tr v-for="item in list" :key="item.id">
        <td>{{ item.id }}</td>
        <td>{{ item.bookname }}</td>
        <td>{{ item.author }}</td>
        <td>{{ item.publisher }}</td>
        <td style="text-align: center">
          <button @click.prevent="details(item.id)">详情</button
          ><button @click="handledel(item.id)">删除</button>
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      bookname: "",
      list: [],
      bookObj: {
        // 参数名提前和后台的参数名对上-发送请求就不用再次对接了
        bookname: "",
        author: "",
        publisher: "",
      },
    };
  },
  created() {
    this.handledata();
    // this.handleAdd();
    // this.handeldetails();
  },
  methods: {
    //删除数据
    handledel(val) {
      console.log(val);
      let params = { id: val };
      this.$axios({
        url: "/api/delbook",
        params,
      }).then((res) => {
        if (res.data.status !== 200) return alert(res.data.msg);
        this.handledata();
      });
    },
    //获取接口数据
    handledata() {
      let params = {
        bookname: this.bookname,
      };
      this.$axios({
        url: "/api/getbooks",
        params: (params = params.bookname ? params : null),
      }).then((res) => {
        console.log(res.data.data);
        if (res.data.status !== 200) return alert(res.data.msg);
        this.list = res.data.data;
        // this.handleAdd();
      });
    },
    //新增
    handleAdd() {
      this.$axios({
        url: "/api/addbook",
        method: "POST",
        data: {
          ...this.bookObj,
          appkey: "7250d3eb-18e1-41bc-8bb2-11483665535a",
        },
      }).then((res) => {
        if (res.data.status !== 200) return alert(res.data.msg);
        console.log(res);
        this.handledata();
      });
    },
    addBook() {
      this.handleAdd();
    },

    //详情
    handeldetails(id) {
      this.$axios({
        url: "/api/getbooks",
        params: { id },
      }).then((res) => {
        console.log(res.data.data);
        const info = res.data.data && res.data.data[0];
        alert(
          `书名：${info.bookname}; 作者：${info.author}; 出版社：${info.publisher}`
        );
      });
    },
    search() {
      this.handledata();
    },
    details() {
      // console.log(111);
      this.handeldetails();
    },
  },
  // watch: {
  //   arr: {
  //     deep: true,
  //     handledata() {
  //       this.$axios({
  //         url: "/api/getbooks",
  //       }).then((res) => {
  //         this.arr = res.data.data;
  //         console.log(111);
  //       });
  //     },
  //   },
  // },
};
</script>

<style lang="less" scoped>
#app {
  width: 1000px;
  height: 1000px;
  margin: 0 auto;
  #Navigation {
    width: 1000px;
    height: 50px;
    background-color: pink;
    display: flex;
    .search {
      width: 260px;
      height: 30px;
      background: red;
      padding-top: 16px;
      padding-left: 5px;
      input {
        width: 200px;
        height: 20px;
      }
    }
    .add {
      display: flex;
      width: 680px;
      height: 30px;
      background-color: yellow;
      padding-top: 16px;
      padding-left: 5px;
      input {
        width: 200px;
        height: 20px;
        // padding-left: 5px;
      }
      a {
        // background-color: #fff;
      }
    }
  }
  // background: pink;
  .book {
    margin: 0 auto;
    tr {
      th {
        width: 200px;
      }
    }
  }
}
</style>
