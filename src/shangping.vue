<template>
  <div>
    <table border="1" width="700" style="border-collapse: collapse">
      <caption>
        购物车
      </caption>
      <thead>
        <tr>
          <th><input type="checkbox" v-model="isAll" /> <span>全选</span></th>
          <th>名称</th>
          <th>价格</th>
          <th>数量</th>
          <th>总价</th>
          <th>操作</th>
        </tr>
      </thead>
      <tbody>
        <MyTr v-for="(obj, index) in goodList" :key="index" :list="obj"></MyTr>
      </tbody>
      <tfoot>
        <tr>
          <td>合计:{{ count }}总价：{{ sum }}</td>
          <td colspan="5"></td>
        </tr>
      </tfoot>
    </table>
  </div>
</template>

<script>
import MyTr from './components/MyTr.vue';

export default {
  data() {
    return {
      goodList: [
        {
          name: '诸葛亮',
          price: 1000,
          num: 1,
          checked: false,
        },
        {
          name: '蔡文姬',
          price: 1500,
          num: 1,
          checked: false,
        },
        {
          name: '妲己',
          price: 2000,
          num: 1,
          checked: false,
        },
        {
          name: '鲁班',
          price: 2200,
          num: 1,
          checked: false,
        },
      ],
    };
  },
  components: {
    MyTr,
  },
  computed: {
    count() {
      return this.goodList.reduce((sum, next) => (sum += next.num), 0);
    },
    sum() {
      return this.goodList.reduce(
        (sum, next) => (sum += next.num * next.price),
        0
      );
    },
    isAll: {
      get() {
        // console.log(this.goodList.every((ele) => ele.checked));
        return this.goodList.every((ele) => ele.checked);
      },
      set(val) {
        // console.log(val);
        this.goodList.forEach((ele) => (ele.checked = val));
      },
    },
  },
};
</script>

<style></style>
