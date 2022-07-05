<template>
  <div>
    <input
      type="text"
      placeholder="搜索-书本名称"
      v-model.trim="bookname"
      @keydown.enter="getbooks"
    /><button @click="returns">返回列表</button>
    <br />
    <br />
    <form>
      请输入要添加的书名：
      <input type="text" placeholder="书名" v-model="booknames" />
      <br />
      <br />
      <br />
      请输入要添加的作者：<input
        type="text"
        placeholder="作者"
        v-model="author"
      />
      <br />
      <br />
      请输入要添加的出版社：<input
        type="text"
        placeholder="出版社"
        v-model="publisher"
      />
      <button ref="btn" @click.prevent="add">创建</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      bookname: '',
      bookList: [],
      author: '',
      booknames: '',
      publisher: '',
    };
  },
  methods: {
    getbooks(flag = true) {
      let params = {};
      if (flag) {
        if (this.bookname.length == 0) return alert('请正确输入！');
        params = { bookname: this.bookname };
      }
      this.$axios({
        url: '/api/getbooks',
        params: params,
      }).then((res) => {
        this.bookList = res.data.data;
        // console.log(this.bookList);
        // console.log(res.data.data);
        this.$emit('newList', this.bookList);
        this.bookname = '';
      });
      // console.log(this.bookname);
    },
    returns() {
      this.getbooks(false);
    },
    add() {
      this.$refs.btn.disabled = true;
      this.$axios({
        url: '/api/addbook',
        method: 'POST',
        data: {
          bookname: this.booknames,
          author: this.author,
          publisher: this.publisher,
        },
      }).then((res) => {
        // console.log(res);
        if (res.status == 200) {
          this.getbooks(false);
        } else {
          alert('添加失败！');
        }
        this.$refs.btn.disabled = false;
        this.booknames = '';
        this.author = '';
        this.publisher = '';
      });
    },
  },
};
</script>

<style scoped>
button {
  margin-left: 10px;
  height: 50px;
  width: 50px;
}
</style>
